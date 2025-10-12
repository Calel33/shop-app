# 📚 API Reference

## 🔗 Base URL

```
Local: http://localhost:3000
Deployed: https://<your-vercel-deployment-domain>
```

## 🔐 Authentication

- App authentication: Clerk handles session auth; protected routes are enforced via `middleware.ts` using `@clerk/nextjs/server`.
- Convex auth: Convex uses Clerk-issued JWTs (JWT template named "convex") to identify users server-side.
- Webhooks: Clerk → Convex webhook requests are signed via Svix; verified using `CLERK_WEBHOOK_SECRET`. Required headers:
  - svix-id
  - svix-timestamp
  - svix-signature

## 📋 API Endpoints

### Webhooks

#### Clerk Users & Billing Webhook

**Request**: `POST /clerk-users-webhook`

**Description**: Receives Clerk webhooks and updates Convex:
- user.created / user.updated → upsert user in `users` table
- user.deleted → delete user from `users`
- paymentAttempt.updated → persist payment attempt in `paymentAttempts` and link to user if found

**Parameters**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| svix-id | header | Yes | Svix event id |
| svix-timestamp | header | Yes | Svix timestamp |
| svix-signature | header | Yes | Svix signature for request verification |

**Request Body (paymentAttempt.updated excerpt)**:
```json
{
  "type": "paymentAttempt.updated",
  "data": {
    "payment_id": "pay_123",
    "status": "paid",
    "payer": { "user_id": "user_abc", "email": "john@doe.com", "first_name": "John", "last_name": "Doe" },
    "payment_source": { "card_type": "visa", "last4": "4242" },
    "billing_date": 1733606400,
    "created_at": 1733606400,
    "updated_at": 1733607400,
    "invoice_id": "inv_123",
    "statement_id": "st_123",
    "subscription_items": [
      {
        "amount": { "amount": 1200, "amount_formatted": "$12.00", "currency": "USD", "currency_symbol": "$" },
        "plan": { "id": "plan_basic", "name": "Basic", "slug": "basic", "amount": 1200, "currency": "USD", "period": "month", "interval": 1 },
        "status": "active",
        "period_start": 1733606400,
        "period_end": 1736198400
      }
    ],
    "totals": {
      "grand_total": { "amount": 1200, "amount_formatted": "$12.00", "currency": "USD", "currency_symbol": "$" },
      "subtotal": { "amount": 1200, "amount_formatted": "$12.00", "currency": "USD", "currency_symbol": "$" },
      "tax_total": { "amount": 0, "amount_formatted": "$0.00", "currency": "USD", "currency_symbol": "$" }
    }
  }
}
```

**Response**:
```json
// 200 OK
null
```

**Status Codes**:
- `200` - Success
- `400` - Bad Request
- `401` - Unauthorized
- `404` - Not Found
- `500` - Server Error

### Convex Functions (Client SDK)

Convex APIs are consumed via the generated client in `convex/_generated/api`. Example public query:

#### users.current (Query)

**Request**: Client SDK via React hook

**Description**: Returns the current authenticated Convex user record or `null`.

**Parameters**:
| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| — | — | — | No args |

**Response**:
```json
{
  "_id": "some_id",
  "name": "Jane Doe",
  "externalId": "user_abc"
}
```

## 🔧 Error Handling

- Webhook requests are verified using Svix. Invalid or missing signatures return `400`.
- Convex internal mutations handle upsert/update idempotently to avoid duplicates (e.g., `paymentAttempts` by `payment_id`).
- Protected routes are enforced by Clerk; unauthorized access to `/dashboard(.*)` results in redirect or `401`/`403` depending on context.

## 📝 Examples

### React: Fetch current user via Convex

```tsx
'use client'
import { useQuery } from 'convex/react'
import { api } from '@/convex/_generated/api'

export default function CurrentUser() {
  const user = useQuery(api.users.current, {})
  if (user === undefined) return <div>Loading...</div>
  if (user === null) return <div>Not signed in</div>
  return <div>Hello, {user.name}</div>
}
```

### Webhook: Required headers (illustrative)
```http
POST /clerk-users-webhook HTTP/1.1
Host: localhost:3000
svix-id: msg_123
svix-timestamp: 1733606400
svix-signature: v1,xxx
Content-Type: application/json

{ ...clerk event payload... }
```

---

*Last updated: 2025-10-08*

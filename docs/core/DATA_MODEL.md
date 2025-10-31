# Data Model

This document describes the core data entities, indexes, and relationships across the database (Convex), service layer (webhooks, queries/mutations), and relevant UI data.

## Entities

- User (Convex: users)
  - _id (PK)
  - name: string
  - externalId: string (UK) — maps to Clerk user id
  - Indexes: byExternalId(externalId)

- PaymentAttempt (Convex: paymentAttempts)
  - _id (PK)
  - payment_id: string (UK)
  - statement_id: string
  - status: string
  - billing_date, created_at, updated_at, paid_at?, failed_at?: number
  - charge_type: string
  - invoice_id: string
  - userId?: id(users) (FK → users._id)
  - payer: { email, first_name, last_name, user_id }
  - payment_source: { card_type, last4 }
  - subscription_items: [{ amount, plan, status, period_start, period_end }]
  - totals: { grand_total, subtotal, tax_total }
  - Indexes: byPaymentId(payment_id), byUserId(userId), byPayerUserId(payer.user_id)

- ClerkUser (external system)
  - id (PK)
  - email, first_name, last_name

## ERD

```mermaid
erDiagram
  CLERK_USER {
    string id PK
    string email
    string first_name
    string last_name
  }

  APP_USER {
    string _id PK
    string name
    string externalId
  }

  PAYMENT_ATTEMPT {
    string _id PK
    string payment_id
    string statement_id
    string status
    int billing_date
    int created_at
    int updated_at
    int paid_at
    int failed_at
    string charge_type
    string invoice_id
    string userId FK
  }

  PAYER {
    string user_id
    string email
    string first_name
    string last_name
  }

  PAYMENT_SOURCE {
    string card_type
    string last4
  }

  SUBSCRIPTION_ITEM {
    int period_start
    int period_end
    string status
  }

  PLAN {
    string id
    string name
    string slug
    number amount
    string currency
    string period
    number interval
  }

  AMOUNT {
    int amount
    string amount_formatted
    string currency
    string currency_symbol
  }

  CLERK_USER ||--|| APP_USER : syncs
  APP_USER ||--o{ PAYMENT_ATTEMPT : has
  PAYMENT_ATTEMPT ||--|| PAYER : contains
  PAYMENT_ATTEMPT ||--|| PAYMENT_SOURCE : contains
  PAYMENT_ATTEMPT ||--o{ SUBSCRIPTION_ITEM : has
  SUBSCRIPTION_ITEM ||--|| PLAN : plan
  SUBSCRIPTION_ITEM ||--|| AMOUNT : amount
  PAYMENT_ATTEMPT ||--|| AMOUNT : grand_total
  PAYMENT_ATTEMPT ||--|| AMOUNT : subtotal
  PAYMENT_ATTEMPT ||--|| AMOUNT : tax_total
```

## Service Layer Mapping

- Webhook (POST /clerk-users-webhook)
  - user.created|updated → users.upsertFromClerk(data)
  - user.deleted → users.deleteFromClerk(clerkUserId)
  - paymentAttempt.updated → paymentAttempts.savePaymentAttempt(transformWebhookData(data))
- Linking rule: paymentAttempts.userId resolves from payer.user_id mapped to users.externalId.

## UI Data

- Public landing/pricing reads static pricing config (CustomClerkPricing).
- Payment-gated areas can query PaymentAttempt(s) by current user; Clerk session + middleware protect dashboard routes.

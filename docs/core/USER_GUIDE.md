# 📖 User Guide

## 🎯 Introduction

Starter.diy is a SaaS starter that gives you authentication, subscriptions, and a real-time backend out of the box. Use it to launch production-quality apps rapidly with a modern UI.

## 🚀 Getting Started

### Account Setup

1. Visit the app and click Sign Up
2. Choose email/password or social provider (as configured in Clerk)
3. Complete verification steps if prompted

### First Login

After sign-in, you’ll be redirected to `/dashboard`. If you are not subscribed, subscription-only pages will be gated until you purchase a plan.

## 📋 Main Features

### Feature 1: Authentication & Protected Dashboard

Secure access to `/dashboard(.*)` via Clerk.

#### How to Use

1. Click Sign In from the landing page
2. Complete auth via Clerk UI
3. Navigate to `/dashboard` (protected content)

#### Tips & Tricks

- If you see a 403 or redirect loop, verify your environment variables and Clerk JWT template.

### Feature 2: Subscription-Gated Content

Billing is powered by Clerk Billing; gated pages are under `/dashboard/payment-gated`.

#### How to Use

1. From the landing page, review plans in the pricing section
2. Select a plan and complete checkout
3. Return to `/dashboard/payment-gated` to access content

#### Tips & Tricks

- Payment status updates are near-real-time via Clerk webhooks → Convex.
- If access doesn’t unlock, wait briefly or refresh; verify webhook configuration.

## 🔧 Settings & Configuration

### Profile Settings

- Manage your profile, sessions, and security through Clerk’s hosted UI components present in the app.

### Preferences

- Toggle dark/light theme; the app respects system preference and can be switched via the UI (powered by `next-themes`).

## 🔍 Troubleshooting

### Common Issues

#### Issue 1: Sign-in redirects back to landing

**Solution**: Ensure Clerk env variables are set and the domain matches your Clerk configuration.

#### Issue 2: Can’t access `/dashboard` (403)

**Solution**: Confirm you’re signed in and that `middleware.ts` is running (correct Next.js matcher).

#### Issue 3: Subscription not unlocking gated page

**Solution**: Check that Clerk webhooks are configured and `CLERK_WEBHOOK_SECRET` is set in Convex.

## 📞 Support

- Use the repository’s issue tracker to report problems and request features.
- Include environment details and logs for faster resolution.

## ❓ FAQ

**Q: Do I need a server for the backend?**  
A: No. Convex provides the serverless backend and real-time database.

**Q: How are payments handled?**  
A: Clerk Billing manages subscription creation, billing cycles, and payment methods; the app receives updates via webhooks.

---

*Last updated: 2025-10-08*

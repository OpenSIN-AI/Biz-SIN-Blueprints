# 📱 WEB APP (SAAS) MODULE (ADD-ON)

**Usage:** Append this to `BLUEPRINT.md` if building a SaaS Web App.

## 💻 SAAS ARCHITECTURE

### 1. Core Components
- **Auth & Multi-tenancy:** Organization-based data isolation.
- **Subscription Management:** Stripe Billing / LemonSqueezy.
- **Dashboard:** Analytics & User Management.

### 2. Database Schema (Prisma/SQL)
```sql
model Organization {
  id          String   @id @default(cuid())
  name        String
  plan        String   // FREE, PRO, ENTERPRISE
  users       User[]
}

model User {
  id          String   @id @default(cuid())
  email       String   @unique
  orgId       String
  role        String   // ADMIN, MEMBER
}
```

### 3. Critical Integrations
- **Emails:** Resend (Transactional)
- **Analytics:** PostHog / Mixpanel
- **Support:** Intercom / Crisp

### 4. Security Requirements
- **RBAC:** Role-Based Access Control enforced on API level.
- **Audit Logs:** Track every critical user action.

# 🛒 E-COMMERCE MODULE (ADD-ON)

**Usage:** Append this to `BLUEPRINT.md` if building a Webshop.

## 🛍️ E-COMMERCE ARCHITECTURE

### 1. Core Components
- **Product Catalog:** PIM (Product Information Management) system.
- **Cart & Checkout:** Persistent cart (Redis) + Stripe Checkout.
- **Order Management:** OMS (Order Management System) via n8n workflows.

### 2. Database Schema (Prisma/SQL)
```sql
model Product {
  id          String   @id @default(cuid())
  name        String
  slug        String   @unique
  price       Decimal
  inventory   Int
  images      String[]
}

model Order {
  id          String   @id @default(cuid())
  userId      String
  total       Decimal
  status      String   // PENDING, PAID, SHIPPED
  items       OrderItem[]
}
```

### 3. Critical Integrations
- **Payments:** Stripe / PayPal / Adyen
- **Shipping:** ShipStation / EasyPost
- **Tax:** Avalara / Stripe Tax

### 4. Performance Requirements
- **LCP (Largest Contentful Paint):** < 2.5s (Critical for SEO)
- **Search:** Algolia / Meilisearch for < 50ms results.

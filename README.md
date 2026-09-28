# Autonomous Shop – Multi-Tenant 24/7 Booking + Interactive Ad Capsules

Fully editable neon-rimmed platform. One-click claim from the map creates a tenant. Admin can edit every outward-facing text and image. Customer page and floating ad capsules are driven 100% by those fields. Every interaction writes a lead and pulses the neon ring.

## Quick Start (works first time)

1. **Clone / open this folder**

2. **Install**
   ```bash
   npm install
   npm install @supabase/supabase-js @supabase/ssr lucide-react clsx tailwind-merge uuid date-fns
   ```

3. **Supabase**
   - Create a free project at supabase.com
   - Go to SQL Editor → paste and run the entire contents of `scripts/seed.sql`
   - Storage → create a public bucket named `tenant-assets`
   - Project Settings → API → copy URL + anon key + service_role key

4. **Environment**
   ```bash
   cp .env.local.example .env.local
   ```
   Fill in:
   ```
   NEXT_PUBLIC_SUPABASE_URL=...
   NEXT_PUBLIC_SUPABASE_ANON_KEY=...
   SUPABASE_SERVICE_ROLE_KEY=...
   NEXT_PUBLIC_APP_URL=http://localhost:3000
   ```
   (Mapbox token is optional – the map falls back to a pin grid)

5. **Run**
   ```bash
   npm run dev
   ```
   Open http://localhost:3000

## What you will see

- **/** – Territory map with 10 local businesses. Click any pin → Claim Free App.
- Claim creates a tenant, links the business, creates a default ad capsule, and redirects you to the Admin dashboard.
- **Admin** – Full content editor (every headline, body, image, neon color). Save → customer page and capsules update.
- **Customer** – Outward-facing page driven by the content you just edited + photo estimator stub + map highlight stub + booking form.
- **Employee** – Lead list for that business.
- **/ad/[capsuleId]** – Fully interactive click-funnel capsule. Every click/hover/submit is recorded.
- **/master** – Global master dashboard (all tenants + leads).

## Editing the outward screens

1. Go to `/app/[slug]/admin`
2. Change any text field or upload a new image
3. Click **Save All Changes**
4. Open `/app/[slug]/customer` or the live capsule link – the new content is live.

## File map

```
src/
  app/
    page.tsx                    # Public map
    claim/[businessId]/route.ts # One-click provision
    app/[tenantSlug]/
      layout.tsx                # Neon shell + role nav
      admin/page.tsx            # Editor + leads
      employee/page.tsx
      customer/page.tsx         # Fully content-driven
    ad/[capsuleId]/page.tsx     # Interactive capsule
    master/page.tsx             # Global view
  components/
    NeonPerimeter.tsx
    ContentEditor.tsx
    EditableImage.tsx
    BookingEngine.tsx
    MapPins.tsx
    CustomerTools.tsx
    CapsuleClient.tsx
    InteractionTracker.tsx
    ClaimButton.tsx
  hooks/useRealtimePulse.ts
  lib/
    types.ts
    supabase/client.ts
    supabase/server.ts
    supabase/admin.ts
scripts/seed.sql
```

## Next improvements

- Real Mapbox GL map with radius filter
- Vision model for the estimator
- Mapbox Draw polygon + area pricing
- Proper auth + RLS tightening
- Email / push notifications on new lead

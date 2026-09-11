# DAT Events — Owner-Control Website

This package upgrades the visual DAT Events site into a real business website with a secure owner dashboard.

## What the owner can control
- Business name, tagline, description, phone and address
- Google rating/review count shown on the site
- Hero/logo image URLs
- WhatsApp number
- Services
- Menu/products
- Future inquiries/orders can be managed from the database

## Architecture
- Public website: `index.html`
- Owner login/dashboard: `admin/index.html`
- Database/auth: Supabase
- Security: Supabase Row Level Security (RLS)
- Designed so you can add more businesses later and keep yourself as `super_admin`.

## Setup
1. Create a Supabase project.
2. Open SQL Editor and run `supabase/schema.sql`.
3. In Supabase Authentication, create the business owner's account.
4. Copy the owner's Auth User ID.
5. In SQL Editor run:
   `update public.businesses set owner_id='OWNER_UUID' where slug='dat-events';`
6. Create the profile link:
   `insert into public.profiles(id, role, business_id) select 'OWNER_UUID','owner',id from public.businesses where slug='dat-events';`
7. Open `config.js` and replace `YOUR_SUPABASE_URL` and `YOUR_SUPABASE_ANON_KEY` with the project's values.
8. Upload the whole folder to your hosting/deployment service.
9. Owner logs in at `/admin/`.

IMPORTANT: never put the Supabase service-role key in this website. Only use the anon/public key in `config.js`.

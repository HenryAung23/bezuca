# Bezuca

A multi-vendor marketplace for digital products (templates, courses, software, music, presets…), built with React Native + Expo (SDK 58) and Expo Router.

## Run it

```bash
npm install
npx expo start          # press "a" for Android, or scan the QR code with Expo Go
npx expo start --web    # browser preview
```

Build an installable Android app with EAS:

```bash
npx eas-cli@latest build -p android --profile preview
```

## Features

**Buyers:** Discover feed (featured carousel, categories, trending, top creators, new arrivals) · search with category, price and sort filters · product pages with pay-what-you-want pricing, files, highlights and reviews · cart and checkout · library with downloads, license keys and reviews · wishlist · follow creators.

**Creators:** one-tap store setup · dashboard with balance, revenue/net/sales stats and a revenue chart · product editor (cover, category, fixed or pay-what-you-want price, file upload via document picker, highlights, draft/publish, delete) · public storefront · sales history · payout method.

**General:** light/dark/system themes, data saved on the device, haptics.

## Project layout

```
src/
  app/            routes (Expo Router)
    (tabs)/       Discover, Search, Library, Sell, Profile
    auth/         welcome + sign-in/up
    product/[id]  creator/[id]  library/[id]
    cart, checkout, success, editor, edit-profile, sales
  components/     UI kit, product cards/covers, charts, sales rows
  data/           types + seed catalogue (6 creators, 12 products)
  store/          Zustand store (persisted with AsyncStorage) + selectors
  theme/          colours, spacing, type, useTheme()
  lib/            formatting helpers
```

## Demo-mode pieces to replace before launch

| Area | Now | Replace with |
| --- | --- | --- |
| Auth | Account stored on the device (`store/useStore.ts → signIn`) | Supabase / Firebase / Clerk |
| Catalogue & sales | Seed data + local store | Backend API / database |
| Payments | Simulated in `app/checkout.tsx` | Stripe (Payment Sheet / Google Pay) + Stripe Connect for creator payouts |
| File delivery | Simulated download in `app/library/[id].tsx` | Signed URLs from object storage (S3, R2, Supabase Storage) |
| "Load demo sales" | Generates fake sales for your own products | Remove once real orders exist |

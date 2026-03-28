# Itzem — Modern Classified Ads Marketplace

A production-ready Next.js classified ads platform inspired by OLX, built for the Pakistani market.

## 🚀 Quick Start

```bash
# 1. Install dependencies
npm install

# 2. Run development server
npm run dev

# 3. Open in browser
# http://localhost:3000
```

## 📁 Project Structure

```
src/
├── app/
│   ├── page.tsx              # Homepage (Hero, Categories, Featured Ads)
│   ├── listings/
│   │   ├── page.tsx          # Listings page (Grid + Filters)
│   │   └── [id]/
│   │       └── page.tsx      # Ad detail page
│   ├── layout.tsx            # Root layout
│   ├── globals.css           # Global styles + fonts
│   └── not-found.tsx         # 404 page
├── components/
│   ├── Navbar.tsx            # Sticky header with search
│   ├── ListingCard.tsx       # Reusable ad card
│   └── Footer.tsx            # Site footer
└── lib/
    └── mockData.ts           # All mock data + types
```

## 🎨 Design Choices

- **Fonts**: Sora (headings) + Plus Jakarta Sans (body)
- **Colors**: Dark ink base, warm orange/amber accent (#f97316)
- **Theme**: Trust-first marketplace — clean whites, subtle shadows, no clutter
- **Locale**: Pakistani rupee (PKR), major cities, realistic listings

## 📱 Pages

| Page | URL |
|------|-----|
| Homepage | `/` |
| Browse Listings | `/listings` |
| Ad Detail | `/listings/[id]` |

## ✅ Features

- Responsive across all screen sizes
- Sticky navbar with mobile hamburger menu  
- Category filtering (client-side)
- City + condition + price range filters
- WhatsApp contact button on every ad
- Featured badge system
- Image gallery with thumbnails
- Seller verification badges
- Safety tips section
- Related ads on detail page

## 🔧 Tech Stack

- **Next.js 14** (App Router)
- **Tailwind CSS** (custom config)
- **TypeScript**
- **Lucide React** (icons)
- **next/image** (optimized images from Unsplash)

## 📦 Build for Production

```bash
npm run build
npm start
```

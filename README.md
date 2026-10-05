# QA Website — Next.js + Sanity CMS

A full-stack marketing/agency website built with **Next.js 16** and **Sanity v4** as a headless CMS. The site features a dynamic home page, a blog with individual post pages, and an embedded Sanity Studio for content management.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Framework | Next.js 16 (App Router) |
| CMS | Sanity v4 (embedded Studio at `/studio`) |
| Styling | Tailwind CSS v4 |
| Rich Text | `@portabletext/react` |
| Images | `@sanity/image-url` |
| Language | JavaScript (ES Modules) |

---

## Features

- **Home page** with Hero, Portfolio, Services, Testimonials, and Blog sections — all content-driven from Sanity
- **Blog listing page** (`/blog`) with Incremental Static Regeneration (ISR, 60s revalidation)
- **Individual blog post pages** (`/blog/[slug]`) with full portable-text rendering
- **Embedded Sanity Studio** at `/studio` with Vision plugin for GROQ querying
- **Dynamic Navbar & Footer** — navigation links and logo pulled from `siteSettings` in Sanity
- **Featured content filtering** — services, portfolio items, and testimonials support a `featured` flag

---

## Sanity Content Schema

| Schema Type | Description |
|---|---|
| `pageSettings` | Home page hero title, subtitle, image, and CTA |
| `siteSettings` | Site title, logo, navigation links, social links, contact info, footer text |
| `blogPost` | Title, slug, excerpt, cover image, portable-text body, category, SEO |
| `service` | Title, slug, short description, icon, image, features, order, featured flag |
| `portfolio` | Title, slug, excerpt, cover image, category, featured flag |
| `testimonial` | Name, company, role, image, message, rating, featured flag |
| `teamMember` | Team member profiles |

---

## Project Structure

```
app/
  page.js                  # Home page (server component)
  blog/
    page.js                # Blog listing (ISR)
    [slug]/page.js         # Individual blog post
  studio/[[...tool]]/      # Embedded Sanity Studio
components/
  Navbar.js
  Footer.js
  home/                    # HeroSection, ServicesSection, PortfolioSection,
  │                        #   TestimonialsSection, BlogSection
  blog/
    BlogList.js
sanity/
  schemaTypes/             # All Sanity schema definitions
  lib/
    client.js              # Sanity client
    queries.js             # GROQ queries
    image.js               # Image URL builder
    live.js                # Live preview helper
  env.js                   # Env var exports
  structure.js             # Studio desk structure
sanity.config.js           # Sanity Studio configuration
```

---

## Getting Started

### 1. Install dependencies

```bash
npm install
```

### 2. Configure environment variables

Create a `.env.local` file in the project root:

```env
NEXT_PUBLIC_SANITY_PROJECT_ID=your_project_id
NEXT_PUBLIC_SANITY_DATASET=production
NEXT_PUBLIC_SANITY_API_VERSION=2026-03-26
```

### 3. Run the development server

```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to view the website.  
Open [http://localhost:3000/studio](http://localhost:3000/studio) to access the Sanity Studio.

---

## Available Scripts

| Command | Description |
|---|---|
| `npm run dev` | Start development server |
| `npm run build` | Build for production |
| `npm run start` | Start production server |
| `npm run lint` | Run ESLint |

---

## Deployment

Deploy to [Vercel](https://vercel.com) in one click — Next.js is optimised for the Vercel platform. Make sure to add the three `NEXT_PUBLIC_SANITY_*` environment variables in your Vercel project settings before deploying.

For Sanity Studio access in production, ensure your production domain is added to the CORS origins in your [Sanity project settings](https://www.sanity.io/manage).

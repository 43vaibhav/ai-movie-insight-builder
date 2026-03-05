# 🎬 AI Movie Insight Builder

A production-ready Next.js application that analyzes any movie using its IMDb ID — fetching real audience reviews and using Gemini AI to generate intelligent sentiment summaries.

![Tech Stack](https://img.shields.io/badge/Next.js-14-black?logo=next.js) ![TypeScript](https://img.shields.io/badge/TypeScript-5-blue?logo=typescript) ![Tailwind CSS](https://img.shields.io/badge/Tailwind-3-38bdf8?logo=tailwindcss) ![Vercel](https://img.shields.io/badge/Deploy-Vercel-black?logo=vercel)

---

## ✨ Features

- **IMDb ID Input** — validated format, quick example shortcuts
- **Movie Details** — poster, title, year, rating, cast, plot via OMDb API
- **Audience Reviews** — up to 50 real reviews from TMDb
- **AI Sentiment Analysis** — Gemini generates a 3–5 sentence summary, sentiment label (Positive / Mixed / Negative), and key themes
- **Heuristic Fallback** — fully functional lexical analysis if no Gemini key is set
- **Skeleton Loaders** — shimmer placeholders during data fetch
- **Framer Motion** — smooth reveal animations throughout
- **Responsive** — mobile-first, works on all screen sizes
- **Error Handling** — user-friendly messages for all failure modes

---

## 🗂 Project Structure

```
/
├── app/
│   ├── components/
│   │   ├── MovieInput.tsx       # IMDb ID form with validation
│   │   ├── MovieCard.tsx        # Movie header (poster, title, rating)
│   │   ├── CastList.tsx         # Cast grid + plot summary
│   │   ├── SentimentSummary.tsx # AI sentiment display + breakdown bars
│   │   ├── ReviewList.tsx       # Paginated review cards
│   │   ├── SkeletonLoader.tsx   # Loading skeleton
│   │   └── ErrorDisplay.tsx     # Error UI
│   ├── lib/
│   │   ├── types.ts             # Shared TypeScript interfaces
│   │   ├── fetchMovie.ts        # OMDb API integration
│   │   ├── fetchReviews.ts      # TMDb reviews API
│   │   └── sentimentAnalyzer.ts # Gemini AI + heuristic fallback
│   ├── layout.tsx
│   └── page.tsx                 # Main app page
├── pages/api/
│   ├── movie.ts                 # GET /api/movie?id=ttXXX
│   └── reviews.ts               # GET /api/reviews?id=ttXXX
├── styles/
│   └── globals.css
├── __tests__/
│   └── sentiment.test.ts        # Vitest tests
└── .env.local.example
```

---

## 🚀 Setup Instructions

### 1. Clone and install

```bash
git clone https://github.com/your-username/ai-movie-insight-builder
cd ai-movie-insight-builder
npm install
```

### 2. Get API keys

| Service | URL | Free Tier |
|---------|-----|-----------|
| OMDb API | https://www.omdbapi.com/apikey.aspx | ✅ 1,000 req/day |
| TMDb API | https://www.themoviedb.org/settings/api | ✅ Unlimited |
| Gemini API | https://aistudio.google.com/ | ✅ Free credits |

### 3. Configure environment

```bash
cp .env.local.example .env.local
# Edit .env.local and fill in your keys
```

### 4. Run locally

```bash
npm run dev
# Open http://localhost:3000
```

### 5. Run tests

```bash
npm test
```

---

## 🧠 How Sentiment Analysis Works

1. **Review Collection** — Up to 50 reviews are fetched from the TMDb reviews API
2. **AI Analysis** (if `GEMINI_API_KEY` is set):
   - Reviews are batched into a prompt (max 25 reviews, ~300 chars each)
   - Gemini returns structured JSON: label, score, summary, breakdown percentages, key themes
3. **Heuristic Fallback** (no API key needed):
   - Each review is tokenized and scanned against curated positive/negative word sets
   - Numeric ratings (if available) boost the score
   - Results are bucketed into Positive / Mixed / Negative thresholds
4. **Display** — Animated breakdown bars + AI-generated (or heuristic) summary paragraph

---

## 🌐 Deployment (Vercel)

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Set environment variables in Vercel dashboard:
# Settings → Environment Variables → add OMDB_API_KEY, TMDB_API_KEY, GEMINI_API_KEY
```

Or use the one-click deploy:

[![Deploy with Vercel](https://vercel.com/button)](https://vercel.com/new)

---

## 🔑 Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `OMDB_API_KEY` | ✅ Yes | OMDb movie data |
| `TMDB_API_KEY` | ✅ Yes | TMDb reviews |
| `GEMINI_API_KEY` | Optional | Gemini sentiment (falls back to heuristic) |

---

## 🛠 Tech Stack

| Layer | Technology |
|-------|-----------|
| Framework | Next.js 14 (App Router + Pages API routes) |
| Language | TypeScript 5 |
| Styling | Tailwind CSS 3 |
| Animation | Framer Motion 11 |
| Movie Data | OMDb API |
| Reviews | TMDb API |
| AI | Google Gemini |
| Testing | Vitest |
| Deployment | Vercel |

---

## 📝 License

MIT

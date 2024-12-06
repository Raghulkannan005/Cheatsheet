# Next.js Comprehensive Guide

Pages & Layouts
Fetching Data
SSG, SSR, ISR
Route Handlers
Build a REST API
Middleware
Revalidation
Mutations

## Project Foundations

### Understanding Next.js

Next.js is a powerful React framework that simplifies web development by providing built-in solutions for routing, rendering, and optimization. It supports both server-side rendering (SSR) and static site generation (SSG), giving developers flexible options for creating high-performance web applications.

### Project Initialization

To start a new Next.js project, you have multiple approaches:

```bash
# NPX (Recommended)
npx create-next-app@latest my-next-project

# Interactive Setup Prompts
? Would you like to use TypeScript? Yes
? Would you like to use ESLint? Yes
? Would you like to use Tailwind CSS? Yes
? Would you like to use `src/` directory? Yes
? Would you like to use App Router? Yes
? Would you like to customize default import aliases? No
```

### Project Structure Breakdown

```plaintext
my-next-project/
│
├── src/                  # Source directory
│   ├── app/              # App Router directory
│   │   ├── layout.tsx    # Root layout
│   │   ├── page.tsx      # Home page
│   │   └── about/
│   │       └── page.tsx  # About page route
│   │
│   ├── components/       # Reusable React components
│   ├── lib/              # Utility functions
│   └── styles/           # Global styles
│
├── public/               # Static assets
├── next.config.js        # Next.js configuration
└── tsconfig.json         # TypeScript configuration
my-next-project/
│
├── src/                  # Source directory
│   ├── app/              # App Router directory
│   │   ├── layout.tsx    # Root layout
│   │   ├── page.tsx      # Home page
│   │   └── about/
│   │       └── page.tsx  # About page route
│   │
│   ├── components/       # Reusable React components
│   ├── lib/              # Utility functions
│   └── styles/           # Global styles
│
├── public/               # Static assets
├── next.config.js        # Next.js configuration
└── tsconfig.json         # TypeScript configuration

```

## Routing Mastery

### Page Routes (App Router)

Next.js 13+ uses a file-system based routing where each file in the `app` directory becomes a route:

```typescript
// src/app/page.tsx
export default function HomePage() {
  return <h1>Welcome to My Next.js App</h1>
}

// src/app/about/page.tsx
export default function AboutPage() {
  return <h1>About Our Company</h1>
}
```

### Dynamic Routes

Create dynamic routes by using square brackets in the file name:

```typescript
// src/app/posts/[slug]/page.tsx
type PostParams = {
  params: { slug: string }
}

export default function PostDetailPage({ params }: PostParams) {
  return <h1>Post: {params.slug}</h1>
}

// Handling multiple dynamic segments
// src/app/products/[category]/[id]/page.tsx
type ProductParams = {
  params: { 
    category: string, 
    id: string 
  }
}

export default function ProductPage({ params }: ProductParams) {
  return (
    <div>
      Category: {params.category}
      Product ID: {params.id}
    </div>
  )
}
```

## Data Fetching Strategies

### Server Components

Next.js 13+ introduces first-class support for server components:

```typescript
// Async server component with direct data fetching
async function fetchUserData() {
  const res = await fetch('https://api.example.com/user', {
    cache: 'no-store'  // Dynamic data
    // OR
    // next: { revalidate: 3600 }  // Cached with periodic revalidation
  })
  return res.json()
}

export default async function ProfilePage() {
  const userData = await fetchUserData()
  return <div>{userData.name}</div>
}
```

### Client-Side Data Fetching

For interactive components, use React hooks:

```typescript
'use client'  // Mandatory for client-side interactions

import { useState, useEffect } from 'react'

export default function ClientDataPage() {
  const [data, setData] = useState(null)

  useEffect(() => {
    async function fetchData() {
      const response = await fetch('/api/data')
      const result = await response.json()
      setData(result)
    }
    fetchData()
  }, [])

  return data ? <div>{data.content}</div> : <p>Loading...</p>
}
```

## Advanced Routing Techniques

### Nested Layouts

```typescript
// src/app/layout.tsx (Root Layout)
export default function RootLayout({ 
  children 
}: { 
  children: React.ReactNode 
}) {
  return (
    <html>
      <body>
        <header>Site Header</header>
        {children}
        <footer>Site Footer</footer>
      </body>
    </html>
  )
}

// src/app/dashboard/layout.tsx
export default function DashboardLayout({ 
  children 
}: { 
  children: React.ReactNode 
}) {
  return (
    <div className="dashboard">
      <SideNavigation />
      <main>{children}</main>
    </div>
  )
}
```

## Performance Optimization

### Static and Dynamic Rendering

```typescript
// Static Generation (Default)
export const dynamic = 'static'

// Server-Side Rendering
export const dynamic = 'force-dynamic'

// Incremental Static Regeneration
export const revalidate = 3600  // Regenerate page every hour
```

## API Routes

```typescript
// src/app/api/users/route.ts
import { NextResponse } from 'next/server'

export async function GET() {
  const users = [{ id: 1, name: 'John' }]
  return NextResponse.json(users)
}

export async function POST(request: Request) {
  const body = await request.json()
  return NextResponse.json({ message: 'User created', data: body })
}
```

## Key Takeaways

1. Next.js simplifies React development with built-in routing and rendering strategies
2. The App Router (13+) provides powerful file-system based routing
3. Server components enable efficient, performant data fetching
4. Flexibility in rendering: static generation, server-side rendering, and client-side rendering

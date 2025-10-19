# 🏗️ Architecture Overview

This document provides a comprehensive overview of the template's architecture, design decisions, and patterns.

## 📊 System Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                         Client Layer                         │
├─────────────────────────────────────────────────────────────┤
│  Next.js App Router (React 19 Server Components)            │
│  ├─ Pages & Layouts                                          │
│  ├─ Client Components (use client)                           │
│  ├─ Server Components (default)                              │
│  └─ API Routes                                               │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                      Presentation Layer                      │
├─────────────────────────────────────────────────────────────┤
│  UI Components (shadcn/ui + Tailwind CSS)                    │
│  ├─ Reusable Components                                      │
│  ├─ Theme Provider (Dark/Light Mode)                         │
│  ├─ Animations (Motion)                                      │
│  └─ Icons (Lucide React)                                     │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                      State Management                        │
├─────────────────────────────────────────────────────────────┤
│  ├─ TanStack Query (Server State)                            │
│  ├─ Zustand (Client State)                                   │
│  └─ React Context (Theme, Auth)                              │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                         API Layer                            │
├─────────────────────────────────────────────────────────────┤
│  tRPC (Type-Safe API)                                        │
│  ├─ Routers (Business Logic)                                 │
│  ├─ Procedures (Queries & Mutations)                         │
│  ├─ Context (Request Context)                                │
│  └─ Middleware (Auth, Logging)                               │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                      Service Layer                           │
├─────────────────────────────────────────────────────────────┤
│  Business Logic & Services                                   │
│  ├─ Authentication Service (Better Auth)                     │
│  ├─ Data Services                                            │
│  └─ External API Integrations                                │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                       Data Layer                             │
├─────────────────────────────────────────────────────────────┤
│  Prisma ORM                                                  │
│  ├─ Schema Definition                                        │
│  ├─ Type Generation                                          │
│  ├─ Query Builder                                            │
│  └─ Migrations                                               │
└─────────────────────────────────────────────────────────────┘
                            ↓
┌─────────────────────────────────────────────────────────────┐
│                       Database                               │
├─────────────────────────────────────────────────────────────┤
│  PostgreSQL 16                                               │
│  ├─ User Management                                          │
│  ├─ Session Storage                                          │
│  ├─ Authentication Data                                      │
│  └─ Application Data                                         │
└─────────────────────────────────────────────────────────────┘
```

## 🔄 Data Flow

### Query Flow (Read Operations)

```
User Interaction
    ↓
React Component
    ↓
tRPC Client Hook (useQuery)
    ↓
HTTP Request (POST /api/trpc)
    ↓
tRPC Server Router
    ↓
Procedure Handler
    ↓
Service Layer (optional)
    ↓
Prisma Query
    ↓
PostgreSQL Database
    ↓
Response Back Through Chain
    ↓
TanStack Query Cache
    ↓
React Component Re-render
```

### Mutation Flow (Write Operations)

```
User Action (Form Submit, Button Click)
    ↓
React Component
    ↓
tRPC Client Hook (useMutation)
    ↓
HTTP Request (POST /api/trpc)
    ↓
tRPC Server Router
    ↓
Input Validation (Zod Schema)
    ↓
Authentication Check (Context)
    ↓
Procedure Handler
    ↓
Service Layer
    ↓
Prisma Mutation
    ↓
PostgreSQL Database
    ↓
Response + Cache Invalidation
    ↓
UI Update
```

## 📁 Directory Structure Explained

```
cms-web/
│
├── app/                          # Next.js App Router
│   ├── api/                      # API Routes
│   │   ├── auth/[...all]/        # Better Auth endpoints
│   │   │   └── route.ts          # Catch-all auth routes
│   │   └── trpc/[trpc]/          # tRPC endpoints
│   │       └── route.ts          # tRPC handler
│   ├── layout.tsx                # Root layout (providers, fonts)
│   ├── page.tsx                  # Home page
│   └── globals.css               # Global styles + Tailwind
│
├── components/                   # React Components
│   ├── ui/                       # shadcn/ui components
│   │   ├── button.tsx
│   │   ├── card.tsx
│   │   └── ...
│   └── theme-provider.tsx        # Dark mode provider
│
├── lib/                          # Utility Libraries
│   ├── auth.ts                   # Better Auth config
│   ├── auth-client.ts            # Client-side auth utils
│   ├── prisma.ts                 # Prisma client instance
│   ├── utils.ts                  # Helper functions (cn, etc.)
│   └── trpc/                     # tRPC Client Config
│       ├── client.ts             # tRPC vanilla client
│       └── provider.tsx          # React Query + tRPC provider
│
├── server/                       # Server-Side Code
│   ├── api/                      # tRPC API
│   │   ├── context.ts            # Request context (user, session)
│   │   ├── trpc.ts               # tRPC instance & procedures
│   │   ├── root.ts               # Root router (combines all)
│   │   └── routers/              # Feature-based routers
│   │       └── job.ts            # Example router
│   ├── services/                 # Business Logic Services
│   └── index.ts                  # Server exports
│
├── prisma/                       # Database
│   ├── schema.prisma             # Database schema
│   └── seed.ts                   # Seed data script
│
├── scripts/                      # Utility Scripts
│   ├── setup-db.sh               # Database setup
│   └── init-project.sh           # Project initialization
│
├── public/                       # Static Assets
│   └── *.svg                     # Images, icons
│
├── .github/                      # GitHub Configuration
│   ├── workflows/                # CI/CD workflows
│   ├── ISSUE_TEMPLATE/           # Issue templates
│   └── pull_request_template.md  # PR template
│
├── docker-compose.yml            # Docker services
├── components.json               # shadcn/ui config
├── tsconfig.json                 # TypeScript config
├── next.config.ts                # Next.js config
├── tailwind.config.ts            # Tailwind config (auto-generated)
├── postcss.config.mjs            # PostCSS config
├── package.json                  # Dependencies & scripts
├── .env.example                  # Environment variables template
├── .env.local                    # Local environment (gitignored)
│
└── Documentation/
    ├── README.md                 # Main documentation
    ├── QUICKSTART.md             # Quick start guide
    ├── TEMPLATE_SETUP.md         # Detailed setup
    ├── DEPLOYMENT.md             # Deployment guide
    ├── ARCHITECTURE.md           # This file
    ├── CONTRIBUTING.md           # Contribution guide
    ├── CHANGELOG.md              # Version history
    ├── HOW_TO_USE_AS_TEMPLATE.md # Template usage guide
    └── LICENSE                   # MIT License
```

## 🔧 Core Technologies

### Frontend Stack

| Technology         | Purpose     | Why?                                       |
| ------------------ | ----------- | ------------------------------------------ |
| **Next.js 15**     | Framework   | Server Components, App Router, Performance |
| **React 19**       | UI Library  | Latest features, Server Components         |
| **TypeScript**     | Type Safety | Catch errors early, better DX              |
| **Tailwind CSS 4** | Styling     | Utility-first, fast development            |
| **shadcn/ui**      | Components  | Accessible, customizable, beautiful        |
| **Motion**         | Animations  | Smooth, performant animations              |
| **Lucide React**   | Icons       | Beautiful, consistent icons                |

### Backend Stack

| Technology      | Purpose        | Why?                                       |
| --------------- | -------------- | ------------------------------------------ |
| **tRPC**        | API Layer      | End-to-end type safety, no code generation |
| **Prisma**      | ORM            | Type-safe database access, migrations      |
| **PostgreSQL**  | Database       | Robust, feature-rich, reliable             |
| **Better Auth** | Authentication | Modern, flexible, secure                   |
| **Zod**         | Validation     | Type-safe schema validation                |

### State Management

| Technology         | Purpose      | Why?                                        |
| ------------------ | ------------ | ------------------------------------------- |
| **TanStack Query** | Server State | Caching, synchronization, automatic refetch |
| **Zustand**        | Client State | Lightweight, simple API, no boilerplate     |
| **React Context**  | Shared State | Theme, auth context                         |

## 🎯 Design Patterns

### 1. Server Components First

```typescript
// Default: Server Component
export default async function Page() {
  // Can fetch data directly
  const data = await prisma.user.findMany();

  return <div>{/* render */}</div>;
}

// Explicit: Client Component
'use client';
export function InteractiveComponent() {
  // Can use hooks, state, events
  const [state, setState] = useState();
  return <button onClick={...}>Click</button>;
}
```

### 2. tRPC Router Pattern

```typescript
// Feature-based routers
export const userRouter = router({
  // Query: Read operation
  list: publicProcedure.query(async () => {
    return await prisma.user.findMany();
  }),

  // Mutation: Write operation
  create: publicProcedure
    .input(z.object({ name: z.string() }))
    .mutation(async ({ input }) => {
      return await prisma.user.create({ data: input });
    }),
});
```

### 3. Context Pattern

```typescript
// Create context with user info
export const createContext = async (opts: CreateNextContextOptions) => {
  const session = await getSession(opts.req);

  return {
    user: session?.user,
    session,
    prisma,
  };
};
```

### 4. Service Layer Pattern

```typescript
// server/services/user.service.ts
export class UserService {
  async createUser(data: CreateUserInput) {
    // Business logic
    // Validation
    // Database operations
    return await prisma.user.create({ data });
  }
}
```

## 🔐 Authentication Flow

```
1. User submits credentials
   ↓
2. POST /api/auth/sign-in
   ↓
3. Better Auth validates credentials
   ↓
4. Password hashed with bcryptjs
   ↓
5. Compare with stored hash
   ↓
6. Create session in database
   ↓
7. Set session cookie
   ↓
8. Return user data
   ↓
9. Client updates auth state
   ↓
10. Redirect to dashboard
```

## 📊 Database Schema

```prisma
User
├─ id (String, CUID)
├─ name (String)
├─ email (String, unique)
├─ emailVerified (Boolean)
├─ image (String?)
├─ createdAt (DateTime)
├─ updatedAt (DateTime)
├─ sessions (Session[])
└─ accounts (Account[])

Session
├─ id (String, CUID)
├─ expiresAt (DateTime)
├─ token (String, unique)
├─ ipAddress (String?)
├─ userAgent (String?)
├─ userId (String, FK)
└─ user (User)

Account
├─ id (String, CUID)
├─ accountId (String)
├─ providerId (String)
├─ userId (String, FK)
├─ accessToken (String?)
├─ refreshToken (String?)
├─ password (String?)
└─ user (User)

Verification
├─ id (String, CUID)
├─ identifier (String)
├─ value (String)
└─ expiresAt (DateTime)
```

## 🚀 Performance Optimizations

### 1. Server Components

- Reduce JavaScript bundle size
- Server-side data fetching
- Automatic code splitting

### 2. TanStack Query Caching

- Automatic background refetch
- Stale-while-revalidate
- Optimistic updates

### 3. Database Connection Pooling

- Reuse connections
- Prevent connection exhaustion
- Better performance under load

### 4. Image Optimization

- Next.js Image component
- Automatic WebP conversion
- Lazy loading

### 5. Route Prefetching

- Automatic prefetching of links
- Faster navigation
- Better UX

## 🔒 Security Considerations

### 1. Authentication

- ✅ Secure password hashing (bcryptjs)
- ✅ Session-based authentication
- ✅ HTTP-only cookies
- ✅ CSRF protection

### 2. Database

- ✅ Parameterized queries (Prisma)
- ✅ SQL injection prevention
- ✅ Connection string in env vars

### 3. API

- ✅ Input validation (Zod)
- ✅ Type safety (TypeScript + tRPC)
- ✅ Context-based authorization

### 4. Environment

- ✅ Secrets in environment variables
- ✅ .env files gitignored
- ✅ Different configs per environment

## 🧪 Testing Strategy

### Recommended Testing Stack

```typescript
// Unit Tests: Vitest
import { describe, it, expect } from "vitest";

describe("UserService", () => {
  it("should create user", async () => {
    // Test logic
  });
});

// Integration Tests: Playwright
import { test, expect } from "@playwright/test";

test("user can sign in", async ({ page }) => {
  // Test flow
});

// E2E Tests: Playwright
test("complete user journey", async ({ page }) => {
  // Full flow test
});
```

## 📈 Scalability Considerations

### Horizontal Scaling

- Stateless server design
- Session in database (not memory)
- Can run multiple instances

### Database Scaling

- Connection pooling
- Read replicas (future)
- Database indexes
- Query optimization

### Caching Strategy

- TanStack Query (client-side)
- Redis (future, server-side)
- CDN for static assets

### Monitoring

- Error tracking (Sentry)
- Performance monitoring
- Database query analysis
- User analytics

## 🔄 Development Workflow

```
1. Create feature branch
   ↓
2. Update Prisma schema (if needed)
   ↓
3. Run migrations: npm run db:migrate
   ↓
4. Create tRPC router
   ↓
5. Add to root router
   ↓
6. Create UI components
   ↓
7. Use tRPC hooks in components
   ↓
8. Test locally
   ↓
9. Commit and push
   ↓
10. Create PR
   ↓
11. Review and merge
   ↓
12. Deploy
```

## 🎨 Styling Architecture

### Tailwind + shadcn/ui Approach

```
Base Styles (globals.css)
    ↓
Tailwind Utilities
    ↓
shadcn/ui Components
    ↓
Custom Components
    ↓
Page-Specific Styles
```

### Theme System

```typescript
// CSS Variables (globals.css)
:root {
  --background: 0 0% 100%;
  --foreground: 0 0% 3.9%;
  --primary: 220 90% 56%;
  // ...
}

// Dark mode
.dark {
  --background: 0 0% 3.9%;
  --foreground: 0 0% 98%;
  // ...
}

// Usage in components
<div className="bg-background text-foreground">
```

## 🔮 Future Enhancements

Potential additions to consider:

- [ ] Redis caching layer
- [ ] WebSocket support (real-time features)
- [ ] Email service integration
- [ ] File upload handling
- [ ] Multi-tenancy support
- [ ] Role-based access control (RBAC)
- [ ] API rate limiting
- [ ] Comprehensive test suite
- [ ] Storybook for components
- [ ] OpenAPI/Swagger docs
- [ ] GraphQL alternative
- [ ] Microservices architecture

## 📚 Learning Resources

To understand this architecture better:

- **Next.js**: [nextjs.org/docs](https://nextjs.org/docs)
- **tRPC**: [trpc.io/docs](https://trpc.io/docs)
- **Prisma**: [prisma.io/docs](https://www.prisma.io/docs)
- **React Server Components**: [react.dev/blog/2023/03/22/react-labs-what-we-have-been-working-on-march-2023](https://react.dev/blog)
- **Better Auth**: [better-auth.com/docs](https://www.better-auth.com/docs)

## 🤝 Contributing

See `CONTRIBUTING.md` for guidelines on improving this architecture.

---

This architecture is designed to be:

- **Scalable**: Grows with your application
- **Maintainable**: Clear separation of concerns
- **Type-Safe**: End-to-end type safety
- **Modern**: Latest best practices
- **Flexible**: Easy to extend and customize

Happy building! 🚀

# Template Setup Guide

This guide will help you set up a new project from this template.

## 🎯 Quick Start (5 minutes)

### Step 1: Create Your Project

**Option A: Using GitHub Template**

1. Click "Use this template" button on GitHub
2. Name your new repository
3. Clone your new repository

**Option B: Manual Clone**

```bash
git clone <template-repo-url> my-new-project
cd my-new-project
rm -rf .git
git init
git add .
git commit -m "Initial commit from template"
```

### Step 2: Customize Project Name

Run these commands to customize your project:

```bash
# Update package.json name
npm pkg set name="my-new-project"

# Update docker-compose.yml (manual edit required)
# Change these values in docker-compose.yml:
# - container_name: my_new_project_db
# - POSTGRES_USER: my_new_project_user
# - POSTGRES_PASSWORD: (generate a secure password)
# - POSTGRES_DB: my_new_project_db
```

### Step 3: Environment Setup

```bash
# Copy environment template
cp .env.example .env.local

# Generate a secure auth secret
openssl rand -base64 32

# Edit .env.local with your values
# Update DATABASE_URL to match your docker-compose.yml settings
```

Example `.env.local`:

```env
DATABASE_URL="postgresql://my_new_project_user:your_secure_password@localhost:5434/my_new_project_db?schema=public"
DATABASE_URL_UNPOOLED="postgresql://my_new_project_user:your_secure_password@localhost:5434/my_new_project_db?schema=public"
BETTER_AUTH_SECRET="your-generated-secret-here"
BETTER_AUTH_URL="http://localhost:3000"
NODE_ENV="development"
```

### Step 4: Install and Setup

```bash
# Install dependencies
npm install

# Setup database (starts Docker, creates schema)
npm run db:setup

# Start development server
npm run dev
```

Visit [http://localhost:3000](http://localhost:3000) - Your app is ready! 🎉

## 🔧 Detailed Customization

### Updating Database Configuration

1. **Edit `docker-compose.yml`:**

```yaml
services:
  postgres:
    container_name: your_project_db
    environment:
      POSTGRES_USER: your_project_user
      POSTGRES_PASSWORD: your_secure_password
      POSTGRES_DB: your_project_db
    ports:
      - "5434:5432" # Change if port conflicts
```

2. **Edit `scripts/setup-db.sh`:**
   Update the database name references in echo statements for clarity.

3. **Update `.env.local`:**
   Match the credentials from docker-compose.yml.

### Customizing Authentication

Edit `lib/auth.ts` to add OAuth providers or customize settings:

```typescript
export const auth = betterAuth({
  database: prismaAdapter(prisma, {
    provider: "postgresql",
  }),
  emailAndPassword: {
    enabled: true,
  },
  // Add OAuth providers
  socialProviders: {
    github: {
      clientId: process.env.GITHUB_CLIENT_ID!,
      clientSecret: process.env.GITHUB_CLIENT_SECRET!,
    },
  },
});
```

### Adding Your First Feature

1. **Create a Prisma Model** (`prisma/schema.prisma`):

```prisma
model Post {
  id        String   @id @default(cuid())
  title     String
  content   String
  published Boolean  @default(false)
  authorId  String
  author    User     @relation(fields: [authorId], references: [id])
  createdAt DateTime @default(now())
  updatedAt DateTime @updatedAt

  @@map("post")
}
```

2. **Update Database:**

```bash
npm run db:push
```

3. **Create tRPC Router** (`server/api/routers/post.ts`):

```typescript
import { z } from "zod";
import { router, publicProcedure } from "../trpc";
import { prisma } from "@/lib/prisma";

export const postRouter = router({
  list: publicProcedure.query(async () => {
    return await prisma.post.findMany({
      include: { author: true },
    });
  }),

  create: publicProcedure
    .input(
      z.object({
        title: z.string(),
        content: z.string(),
      })
    )
    .mutation(async ({ input, ctx }) => {
      return await prisma.post.create({
        data: {
          ...input,
          authorId: ctx.user.id, // from auth context
        },
      });
    }),
});
```

4. **Add to Root Router** (`server/api/root.ts`):

```typescript
import { postRouter } from "./routers/post";

export const appRouter = router({
  post: postRouter,
  // ... other routers
});
```

5. **Use in Components:**

```typescript
"use client";

import { trpc } from "@/lib/trpc/client";

export function PostList() {
  const { data: posts, isLoading } = trpc.post.list.useQuery();

  if (isLoading) return <div>Loading...</div>;

  return (
    <div>
      {posts?.map((post) => (
        <div key={post.id}>
          <h2>{post.title}</h2>
          <p>{post.content}</p>
        </div>
      ))}
    </div>
  );
}
```

## 🎨 Styling Customization

### Change Theme Colors

Edit `app/globals.css`:

```css
@layer base {
  :root {
    --background: 0 0% 100%;
    --foreground: 0 0% 3.9%;
    --primary: 220 90% 56%; /* Change this */
    /* ... other colors */
  }
}
```

### Add shadcn/ui Components

```bash
npx shadcn@latest add button
npx shadcn@latest add card
npx shadcn@latest add form
npx shadcn@latest add input
npx shadcn@latest add dialog
```

## 📦 Adding Dependencies

```bash
# Add a new dependency
npm install package-name

# Add a dev dependency
npm install -D package-name
```

## 🚀 Deployment Checklist

### Pre-Deployment

- [ ] Update `package.json` name and version
- [ ] Set production environment variables
- [ ] Run database migrations
- [ ] Test build locally: `npm run build`
- [ ] Update `BETTER_AUTH_URL` to production URL
- [ ] Generate strong `BETTER_AUTH_SECRET`
- [ ] Set `NODE_ENV=production`

### Vercel Deployment

1. Push to GitHub
2. Import project in Vercel
3. Add environment variables:
   - `DATABASE_URL`
   - `DATABASE_URL_UNPOOLED`
   - `BETTER_AUTH_SECRET`
   - `BETTER_AUTH_URL`
   - `NODE_ENV=production`
4. Deploy

### Database Setup (Production)

**Option 1: Vercel Postgres**

```bash
# Install Vercel Postgres
npm install @vercel/postgres

# Update DATABASE_URL in Vercel dashboard
```

**Option 2: Supabase**

1. Create project on Supabase
2. Get connection string
3. Update `DATABASE_URL` and `DATABASE_URL_UNPOOLED`
4. Run migrations: `npx prisma migrate deploy`

**Option 3: Railway/Render**

1. Create PostgreSQL instance
2. Get connection string
3. Update environment variables
4. Run migrations

## 🔍 Troubleshooting

### Database Connection Issues

```bash
# Check if Docker is running
docker ps

# Restart database
npm run db:restart

# View logs
npm run db:logs

# Reset database (WARNING: deletes data)
npm run db:reset
```

### Port Conflicts

If port 5434 is in use, update:

1. `docker-compose.yml` ports section
2. `.env.local` DATABASE_URL port
3. `scripts/setup-db.sh` connection string

### Prisma Issues

```bash
# Regenerate Prisma client
npm run db:generate

# Reset Prisma client
rm -rf node_modules/.prisma
npm run db:generate
```

### Build Errors

```bash
# Clear Next.js cache
rm -rf .next

# Reinstall dependencies
rm -rf node_modules package-lock.json
npm install

# Rebuild
npm run build
```

## 📚 Next Steps

1. **Read the Documentation**: Check out the main README.md
2. **Explore the Code**: Familiarize yourself with the project structure
3. **Add Features**: Start building your application
4. **Customize UI**: Modify theme and add components
5. **Deploy**: Ship your application to production

## 💡 Tips

- Use `npm run db:studio` to visually inspect your database
- Keep `.env.local` in `.gitignore` (already configured)
- Use TypeScript strictly for better type safety
- Leverage tRPC for type-safe APIs
- Use Prisma migrations in production
- Test locally before deploying

## 🆘 Getting Help

- Check the main README.md for documentation links
- Review official documentation for each technology
- Search GitHub issues in respective repositories
- Join community Discord servers for support

Happy coding! 🚀

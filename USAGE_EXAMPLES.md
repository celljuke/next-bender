# 📖 Usage Examples

Quick reference for using your template in different scenarios.

## 🚀 Creating New Projects

### Option 1: create-next-app (Recommended)

**Basic usage:**

```bash
npx create-next-app@latest my-app -e https://github.com/celljuke/next-bender
cd my-app
./scripts/init-project.sh
npm run dev
```

**With specific branch:**

```bash
npx create-next-app@latest my-app -e https://github.com/celljuke/next-bender/tree/develop
```

**With specific tag/version:**

```bash
npx create-next-app@latest my-app -e https://github.com/celljuke/next-bender/tree/v1.0.0
```

**Short form (if public):**

```bash
npx create-next-app@latest my-app -e celljuke/next-bender
```

### Option 2: GitHub Template Button

1. Visit: `https://github.com/celljuke/next-bender`
2. Click **"Use this template"**
3. Fill in repository details
4. Clone your new repository
5. Run setup:
   ```bash
   git clone https://github.com/celljuke/my-new-repo
   cd my-new-repo
   ./scripts/init-project.sh
   npm run dev
   ```

### Option 3: Manual Clone

```bash
# Clone the template
git clone https://github.com/celljuke/next-bender my-project

# Navigate to project
cd my-project

# Remove git history (optional)
rm -rf .git
git init

# Initialize project
./scripts/init-project.sh

# Start development
npm run dev
```

## 🎯 Real-World Examples

### Example 1: E-commerce Platform

```bash
# Create project
npx create-next-app@latest my-store -e celljuke/next-bender

# Navigate and setup
cd my-store
./scripts/init-project.sh
# Enter project name: my-store
# Setup database: y

# Add e-commerce models
# Edit prisma/schema.prisma
# Add Product, Order, Cart models

# Push to database
npm run db:push

# Start building
npm run dev
```

### Example 2: SaaS Dashboard

```bash
# Create with specific version
npx create-next-app@latest saas-dashboard -e celljuke/next-bender/tree/v1.0.0

cd saas-dashboard
./scripts/init-project.sh

# Add subscription models
# Edit prisma/schema.prisma

npm run db:push
npm run dev
```

### Example 3: Blog Platform

```bash
# Create project
npx create-next-app@latest my-blog -e celljuke/next-bender

cd my-blog
./scripts/init-project.sh

# Add blog models (Post, Comment, Category)
# Create tRPC routers for blog functionality
# Build UI components

npm run dev
```

### Example 4: Internal Tool

```bash
# Create from develop branch
npx create-next-app@latest internal-tool -e celljuke/next-bender/tree/develop

cd internal-tool
./scripts/init-project.sh

# Customize for internal use
# Add company-specific features
# Configure authentication

npm run dev
```

## 🔧 Post-Creation Workflows

### Standard Workflow

```bash
# 1. Create project
npx create-next-app@latest my-app -e celljuke/next-bender

# 2. Setup
cd my-app
./scripts/init-project.sh

# 3. Verify setup
npm run dev
# Visit http://localhost:3000

# 4. Database management
npm run db:studio
# Visual database interface opens

# 5. Start building features
# Edit files, add components, create APIs

# 6. Commit your work
git add .
git commit -m "Initial setup complete"
git push origin main
```

### Advanced Workflow

```bash
# 1. Create with specific version
npx create-next-app@latest my-app -e celljuke/next-bender/tree/v1.2.0

# 2. Setup with custom configuration
cd my-app
./scripts/init-project.sh

# 3. Customize database
# Edit docker-compose.yml for different port
# Update .env.local

# 4. Add custom models
# Edit prisma/schema.prisma

# 5. Generate and migrate
npm run db:generate
npm run db:migrate

# 6. Add custom tRPC routers
# Create files in server/api/routers/

# 7. Add UI components
npx shadcn@latest add button card form input

# 8. Start development
npm run dev
```

## 📦 Team Workflows

### For Team Lead

```bash
# Create project from template
npx create-next-app@latest team-project -e celljuke/next-bender

cd team-project

# Setup with team configuration
./scripts/init-project.sh
# Project name: team-project
# Database: yes

# Configure for team
# Update .env.example with team settings
# Add team-specific documentation

# Push to team repository
git remote add origin https://github.com/team/team-project
git push -u origin main

# Share with team
echo "Team: Clone and run 'npm install && npm run db:setup && npm run dev'"
```

### For Team Members

```bash
# Clone team project
git clone https://github.com/team/team-project
cd team-project

# Install dependencies
npm install

# Setup local database
npm run db:setup

# Start development
npm run dev

# Create feature branch
git checkout -b feature/my-feature
```

## 🌍 Multi-Environment Setup

### Development Environment

```bash
# Create project
npx create-next-app@latest my-app -e celljuke/next-bender
cd my-app
./scripts/init-project.sh

# Use local database (default)
npm run dev
```

### Staging Environment

```bash
# Same project, different .env
cp .env.local .env.staging

# Edit .env.staging with staging database
# DATABASE_URL=postgresql://staging_user:pass@staging-host:5432/staging_db

# Build and test
npm run build
npm run start
```

### Production Environment

```bash
# Deploy to Vercel/other platform
# Set environment variables in platform dashboard

# DATABASE_URL=<production-db>
# BETTER_AUTH_SECRET=<production-secret>
# BETTER_AUTH_URL=https://yourdomain.com
# NODE_ENV=production
```

## 🎨 Customization Examples

### Adding OAuth Authentication

```bash
# Create project
npx create-next-app@latest my-app -e celljuke/next-bender
cd my-app
./scripts/init-project.sh

# Install OAuth providers
npm install @auth/core

# Edit lib/auth.ts
# Add GitHub, Google, etc.

# Update .env.local
# Add OAuth credentials

npm run dev
```

### Adding Stripe Integration

```bash
# Create project
npx create-next-app@latest my-saas -e celljuke/next-bender
cd my-saas
./scripts/init-project.sh

# Install Stripe
npm install stripe @stripe/stripe-js

# Add Stripe models to prisma/schema.prisma
# Create Stripe service in server/services/
# Add Stripe tRPC router

npm run db:push
npm run dev
```

### Adding Email Service

```bash
# Create project
npx create-next-app@latest my-app -e celljuke/next-bender
cd my-app
./scripts/init-project.sh

# Install email service (e.g., Resend)
npm install resend

# Create email service
# Add email templates
# Create email tRPC router

npm run dev
```

## 🚀 Deployment Examples

### Deploy to Vercel

```bash
# Create and setup project
npx create-next-app@latest my-app -e celljuke/next-bender
cd my-app
./scripts/init-project.sh

# Initialize git
git add .
git commit -m "Initial commit"

# Push to GitHub
git remote add origin https://github.com/celljuke/my-app
git push -u origin main

# Deploy to Vercel
npx vercel

# Or use Vercel dashboard to import from GitHub
```

### Deploy with Docker

```bash
# Create project
npx create-next-app@latest my-app -e celljuke/next-bender
cd my-app
./scripts/init-project.sh

# Build Docker image
docker build -t my-app .

# Run container
docker run -p 3000:3000 --env-file .env.production my-app
```

## 📊 Testing Examples

### Local Testing

```bash
# Create project
npx create-next-app@latest my-app -e celljuke/next-bender
cd my-app
./scripts/init-project.sh

# Install testing libraries
npm install -D vitest @testing-library/react @testing-library/jest-dom

# Add test scripts to package.json
# Create test files

# Run tests
npm test
```

### E2E Testing

```bash
# Setup project
npx create-next-app@latest my-app -e celljuke/next-bender
cd my-app
./scripts/init-project.sh

# Install Playwright
npm init playwright@latest

# Write E2E tests
# Create tests/e2e/ directory

# Run E2E tests
npx playwright test
```

## 🔄 Update Workflows

### Updating from Template

```bash
# In your project
cd my-existing-project

# Add template as remote
git remote add template https://github.com/celljuke/next-bender

# Fetch template updates
git fetch template

# Merge specific changes (carefully!)
git cherry-pick <commit-hash>

# Or merge entire branch
git merge template/main --allow-unrelated-histories
```

## 💡 Pro Tips

### Tip 1: Use Specific Versions in Production

```bash
# Always use tagged versions for production
npx create-next-app@latest prod-app -e celljuke/next-bender/tree/v1.0.0
```

### Tip 2: Create Project Variants

```bash
# Minimal variant
npx create-next-app@latest minimal-app -e celljuke/next-bender/tree/minimal

# Full-featured variant
npx create-next-app@latest full-app -e celljuke/next-bender/tree/full
```

### Tip 3: Automate Setup

```bash
# One-liner for complete setup
npx create-next-app@latest my-app -e celljuke/next-bender && cd my-app && ./scripts/init-project.sh && npm run dev
```

### Tip 4: Document Your Customizations

```bash
# After setup, document changes
echo "# Project-Specific Setup" > SETUP.md
echo "- Custom feature X added" >> SETUP.md
echo "- Modified Y for our use case" >> SETUP.md
```

## 📚 Learning Examples

### Example 1: Learning tRPC

```bash
npx create-next-app@latest learn-trpc -e celljuke/next-bender
cd learn-trpc
./scripts/init-project.sh

# Study server/api/routers/job.ts
# Create your own router
# Experiment with queries and mutations
```

### Example 2: Learning Prisma

```bash
npx create-next-app@latest learn-prisma -e celljuke/next-bender
cd learn-prisma
./scripts/init-project.sh

# Study prisma/schema.prisma
# Add new models
# Use Prisma Studio to explore
npm run db:studio
```

### Example 3: Learning Next.js App Router

```bash
npx create-next-app@latest learn-nextjs -e celljuke/next-bender
cd learn-nextjs
./scripts/init-project.sh

# Study app/ directory structure
# Create new routes
# Experiment with Server Components
```

## 🎉 Success Stories

Share how you've used the template:

```bash
# Quick prototype
npx create-next-app@latest prototype -e celljuke/next-bender
# Built MVP in 2 days instead of 2 weeks!

# Client project
npx create-next-app@latest client-project -e celljuke/next-bender
# Delivered ahead of schedule

# Hackathon project
npx create-next-app@latest hackathon -e celljuke/next-bender
# Won first place with fully-functional app!
```

---

## 📞 Quick Command Reference

```bash
# Basic
npx create-next-app@latest APP_NAME -e GITHUB_URL

# Your template
npx create-next-app@latest my-app -e celljuke/next-bender

# With version
npx create-next-app@latest my-app -e celljuke/next-bender/tree/v1.0.0

# Complete setup
npx create-next-app@latest my-app -e celljuke/next-bender && cd my-app && ./scripts/init-project.sh && npm run dev
```

---

**Start building amazing things with your template!** 🚀

# ⚡ Quick Start Guide

Get up and running in 5 minutes!

## 🎯 Prerequisites

- Node.js 20+ installed
- Docker Desktop running
- Terminal/Command line access

## 🚀 Setup Steps

### 1️⃣ Create Your Project

**Using GitHub Template:**

1. Click "Use this template" button on GitHub
2. Name your repository
3. Clone it: `git clone <your-repo-url>`
4. `cd <your-project-name>`

**Or clone directly:**

```bash
git clone <template-url> my-project
cd my-project
```

### 2️⃣ Run Initialization Script

```bash
# Make script executable (if needed)
chmod +x scripts/init-project.sh

# Run the initialization
./scripts/init-project.sh
```

This script will:

- ✅ Update project name
- ✅ Generate secure credentials
- ✅ Create `.env.local`
- ✅ Set up database (optional)

### 3️⃣ Install Dependencies

```bash
npm install
```

### 4️⃣ Start Development

```bash
# If you didn't set up database in step 2
npm run db:setup

# Start the dev server
npm run dev
```

Visit **http://localhost:3000** 🎉

## 📦 What You Get

- ✅ Next.js 15 with App Router
- ✅ TypeScript configured
- ✅ Tailwind CSS + shadcn/ui
- ✅ PostgreSQL database (Docker)
- ✅ Prisma ORM
- ✅ tRPC API layer
- ✅ Authentication (Better Auth)
- ✅ Dark mode support

## 🎨 Add UI Components

```bash
npx shadcn@latest add button
npx shadcn@latest add card
npx shadcn@latest add form
```

## 🗄️ Database Commands

```bash
npm run db:studio    # Open database GUI
npm run db:push      # Push schema changes
npm run db:migrate   # Create migrations
npm run db:seed      # Seed data
```

## 📚 Next Steps

1. **Read the docs**: Check `README.md` for full documentation
2. **Customize**: Update theme in `app/globals.css`
3. **Add features**: Create tRPC routers in `server/api/routers/`
4. **Build**: Start building your app!

## 🆘 Troubleshooting

**Database won't start?**

```bash
docker ps  # Check if Docker is running
npm run db:restart
```

**Port 5434 in use?**

- Change port in `docker-compose.yml` and `.env.local`

**Build errors?**

```bash
rm -rf .next node_modules
npm install
npm run dev
```

## 📖 Full Documentation

- `README.md` - Complete documentation
- `TEMPLATE_SETUP.md` - Detailed setup guide
- `CONTRIBUTING.md` - Contribution guidelines

## 💡 Tips

- Use `npm run db:studio` to visually manage data
- Check `server/api/routers/job.ts` for tRPC example
- Explore `prisma/schema.prisma` for database models
- Authentication is pre-configured in `lib/auth.ts`

Happy coding! 🚀

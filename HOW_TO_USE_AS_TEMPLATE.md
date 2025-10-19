# 📘 How to Use This as a GitHub Template

This guide explains how to set up this repository as a GitHub template and use it for future projects.

## 🎯 What is a GitHub Template?

A GitHub template repository is a special type of repository that can be used as a starting point for new projects. When you create a repository from a template, you get a fresh copy without the original repository's commit history.

## 📋 Setting Up as a Template Repository

### Step 1: Push to GitHub

If you haven't already, push this repository to GitHub:

```bash
# Initialize git (if not already done)
git init

# Add all files
git add .

# Commit
git commit -m "Initial template setup"

# Create a new repository on GitHub, then:
git remote add origin https://github.com/yourusername/nextjs-fullstack-template.git
git branch -M main
git push -u origin main
```

### Step 2: Enable Template Feature

1. Go to your repository on GitHub
2. Click **Settings** (top right)
3. Scroll to the **Template repository** section
4. Check the box: ☑️ **Template repository**
5. Click **Save**

That's it! Your repository is now a template.

### Step 3: Customize Repository Settings (Optional)

While in Settings, you can also:

1. **Add Topics** (helps with discoverability)

   - Click the gear icon next to "About"
   - Add topics: `nextjs`, `react`, `typescript`, `prisma`, `trpc`, `template`, etc.

2. **Update Description**

   - "A production-ready Next.js template with authentication, database, and API layer"

3. **Add Website** (if you have a demo)

   - Link to your deployed demo

4. **Enable Discussions** (optional)
   - For community support

## 🚀 Using Your Template for New Projects

### Method 1: GitHub Web Interface

1. Go to your template repository on GitHub
2. Click the green **"Use this template"** button
3. Select **"Create a new repository"**
4. Fill in:
   - Repository name: `my-new-project`
   - Description: (optional)
   - Public/Private
5. Click **"Create repository"**
6. Clone your new repository:
   ```bash
   git clone https://github.com/yourusername/my-new-project.git
   cd my-new-project
   ```

### Method 2: GitHub CLI

```bash
# Create a new repository from template
gh repo create my-new-project --template yourusername/nextjs-fullstack-template --public

# Clone it
gh repo clone yourusername/my-new-project
cd my-new-project
```

### Method 3: Manual Clone (Not Recommended)

```bash
# Clone the template
git clone https://github.com/yourusername/nextjs-fullstack-template.git my-new-project
cd my-new-project

# Remove git history
rm -rf .git

# Initialize new repository
git init
git add .
git commit -m "Initial commit from template"

# Push to your new repository
git remote add origin https://github.com/yourusername/my-new-project.git
git push -u origin main
```

## 🔧 After Creating from Template

Once you've created a new project from the template, follow these steps:

### 1. Run Initialization Script

```bash
# Make executable
chmod +x scripts/init-project.sh

# Run initialization
./scripts/init-project.sh
```

This will:

- Update project name in `package.json`
- Generate secure credentials
- Update `docker-compose.yml`
- Create `.env.local`
- Optionally set up database

### 2. Or Manually Configure

If you prefer manual setup:

```bash
# Update package.json name
npm pkg set name="my-new-project"

# Copy environment file
cp .env.example .env.local

# Edit .env.local with your values
# Generate auth secret: openssl rand -base64 32

# Update docker-compose.yml
# Change container name, database name, user, password
```

### 3. Install and Setup

```bash
# Install dependencies
npm install

# Setup database
npm run db:setup

# Start development
npm run dev
```

## 📦 Template Maintenance

### Keeping Your Template Updated

To keep your template current:

1. **Regular Updates**

   ```bash
   # Update dependencies
   npm update

   # Check for outdated packages
   npm outdated

   # Update major versions carefully
   npm install package@latest
   ```

2. **Test After Updates**

   ```bash
   npm run build
   npm run dev
   ```

3. **Document Changes**
   - Update `CHANGELOG.md`
   - Update version in `package.json`
   - Commit and push

### Versioning Your Template

Use semantic versioning:

```bash
# Patch: Bug fixes
npm version patch

# Minor: New features
npm version minor

# Major: Breaking changes
npm version major

# Push with tags
git push --follow-tags
```

## 🌟 Making Your Template Public

### Best Practices

1. **Complete Documentation**

   - ✅ Comprehensive README
   - ✅ Setup guide
   - ✅ Deployment guide
   - ✅ Contributing guidelines

2. **Clean Code**

   - ✅ No hardcoded credentials
   - ✅ No personal information
   - ✅ Consistent code style
   - ✅ Comments where needed

3. **Working Examples**

   - ✅ Sample tRPC router
   - ✅ Database models
   - ✅ Authentication setup

4. **Easy Setup**
   - ✅ Initialization script
   - ✅ Clear instructions
   - ✅ Troubleshooting guide

### Promoting Your Template

1. **Add to GitHub Topics**

   - nextjs-template
   - react-template
   - typescript-template
   - fullstack-template

2. **Share on Social Media**

   - Twitter/X
   - Reddit (r/nextjs, r/reactjs)
   - Dev.to
   - Hashnode

3. **Add to Lists**

   - Awesome Next.js
   - Awesome React
   - Template collections

4. **Create a Demo**
   - Deploy to Vercel
   - Add link to repository

## 📊 Template Repository Features

### What Gets Copied

When someone uses your template:

- ✅ All files and folders
- ✅ Branch structure
- ✅ README and documentation
- ✅ Configuration files

### What Doesn't Get Copied

- ❌ Commit history
- ❌ Issues
- ❌ Pull requests
- ❌ GitHub Actions runs
- ❌ Releases

### Template-Specific Files

These files help users of your template:

- `README.md` - Main documentation
- `TEMPLATE_SETUP.md` - Setup instructions
- `QUICKSTART.md` - Quick start guide
- `.env.example` - Environment variables template
- `scripts/init-project.sh` - Initialization script
- `DEPLOYMENT.md` - Deployment guide
- `CONTRIBUTING.md` - Contribution guidelines

## 🔄 Syncing Template Updates

If you want to update projects created from your template:

### For Template Maintainer

```bash
# Create a new branch for updates
git checkout -b template-updates

# Make changes
# Commit changes
git commit -m "Update dependencies and docs"

# Push
git push origin template-updates
```

### For Template Users

Users can manually pull updates:

```bash
# Add template as remote
git remote add template https://github.com/yourusername/nextjs-fullstack-template.git

# Fetch template changes
git fetch template

# Merge specific changes
git cherry-pick <commit-hash>

# Or merge entire branch (careful!)
git merge template/main --allow-unrelated-histories
```

## 🆘 Troubleshooting

### Template Button Not Showing

- Ensure repository is public or you have access
- Check that "Template repository" is enabled in Settings
- Refresh the page

### Users Can't Create from Template

- Repository must be public (or users need access)
- Check repository permissions
- Verify template setting is enabled

### Template Not Appearing in Search

- Add relevant topics
- Make repository public
- Add clear description
- Wait for GitHub indexing

## 📚 Additional Resources

- [GitHub Template Repositories Docs](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository)
- [GitHub Topics](https://github.com/topics)
- [Semantic Versioning](https://semver.org/)

## 🎉 Success!

Your template is now ready to use! Every time you start a new project:

1. Click "Use this template"
2. Run `./scripts/init-project.sh`
3. Start building!

No more copying files or setting up from scratch. Your perfect stack is always one click away! 🚀

---

**Pro Tip**: Keep a checklist of customizations you typically make and add them to the initialization script for even faster setup!

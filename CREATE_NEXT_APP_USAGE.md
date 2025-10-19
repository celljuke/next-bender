# 🚀 Using with create-next-app

Your template can be used with `create-next-app` to quickly bootstrap new projects!

## 📦 Prerequisites

1. **Push to GitHub**: Your template must be in a public GitHub repository
2. **Template Ready**: All files committed and pushed

## 🎯 Usage Methods

### Method 1: Direct GitHub URL (Recommended)

Once your template is on GitHub, anyone can use it with:

```bash
npx create-next-app@latest my-new-project -e https://github.com/yourusername/your-template-repo
```

**Example:**

```bash
npx create-next-app@latest my-awesome-app -e https://github.com/celljuke/nextjs-fullstack-template
```

### Method 2: Short GitHub Path

If your repository is public, you can use the short form:

```bash
npx create-next-app@latest my-new-project -e yourusername/your-template-repo
```

**Example:**

```bash
npx create-next-app@latest my-awesome-app -e celljuke/nextjs-fullstack-template
```

### Method 3: With Specific Branch or Tag

Use a specific branch or tag:

```bash
npx create-next-app@latest my-new-project -e https://github.com/yourusername/your-template-repo/tree/branch-name
```

**Example:**

```bash
npx create-next-app@latest my-awesome-app -e https://github.com/celljuke/nextjs-fullstack-template/tree/v1.0.0
```

## 🔧 Complete Setup Flow

After creating a project with `create-next-app`:

```bash
# 1. Create project from your template
npx create-next-app@latest my-new-project -e https://github.com/yourusername/your-template-repo

# 2. Navigate to project
cd my-new-project

# 3. Run initialization script
chmod +x scripts/init-project.sh
./scripts/init-project.sh

# 4. Start development
npm run dev
```

## 📋 What Gets Installed

When using `create-next-app` with your template:

✅ **Included:**

- All source code
- All configuration files
- All documentation
- All scripts
- `package.json` with dependencies
- `.gitignore`

❌ **Not Included:**

- Git history (fresh git init)
- `node_modules` (installed separately)
- `.env.local` (created by init script)

## 🎨 Customizing for create-next-app

### 1. Add Example Environment File

Already done! Your `.env.example` will be copied by users.

### 2. Update README with Usage

Add this to the top of your README.md:

```markdown
## Quick Start with create-next-app

\`\`\`bash
npx create-next-app@latest my-app -e https://github.com/yourusername/your-template-repo
cd my-app
./scripts/init-project.sh
npm run dev
\`\`\`
```

### 3. Add to package.json

Update your `package.json` description to mention create-next-app usage:

```json
{
  "description": "Production-ready Next.js template. Use with: npx create-next-app -e yourusername/your-template-repo"
}
```

## 🌟 Publishing Your Template

### Step 1: Push to GitHub

```bash
git add .
git commit -m "Template ready for create-next-app"
git push origin main
```

### Step 2: Make Repository Public

1. Go to repository Settings
2. Scroll to "Danger Zone"
3. Click "Change visibility" → "Make public"

### Step 3: Add Topics

Add these topics to your repository for discoverability:

- `nextjs`
- `nextjs-template`
- `create-next-app`
- `typescript`
- `prisma`
- `trpc`
- `template`
- `starter`
- `boilerplate`

### Step 4: Create a Release (Optional)

```bash
git tag -a v1.0.0 -m "Initial release"
git push origin v1.0.0
```

### Step 5: Test It!

```bash
npx create-next-app@latest test-project -e https://github.com/yourusername/your-template-repo
cd test-project
./scripts/init-project.sh
npm run dev
```

## 📚 Documentation Updates

Add this section to your README.md:

```markdown
## 🚀 Quick Start

### Using create-next-app (Fastest)

\`\`\`bash
npx create-next-app@latest my-app -e https://github.com/yourusername/your-template-repo
cd my-app
./scripts/init-project.sh
npm run dev
\`\`\`

### Using GitHub Template

1. Click "Use this template" button
2. Create your repository
3. Clone and run \`./scripts/init-project.sh\`
4. Start coding!
```

## 🎯 Advantages of create-next-app

### ✅ Pros

- **Fast**: Quick project creation
- **Familiar**: Developers know the command
- **Clean**: No git history
- **Simple**: One command to start

### ⚠️ Considerations

- Requires public repository
- Downloads entire repository
- Users need to run init script after

## 🔄 Workflow Comparison

### create-next-app Method

```bash
npx create-next-app@latest my-app -e yourusername/template
cd my-app
./scripts/init-project.sh
npm run dev
```

**Time: ~2 minutes**

### GitHub Template Method

```bash
# On GitHub: Click "Use this template"
git clone https://github.com/yourusername/my-app
cd my-app
./scripts/init-project.sh
npm run dev
```

**Time: ~3 minutes**

### Manual Clone Method

```bash
git clone https://github.com/yourusername/template my-app
cd my-app
rm -rf .git
git init
./scripts/init-project.sh
npm run dev
```

**Time: ~4 minutes**

## 💡 Best Practices

### 1. Keep Main Branch Stable

- Only merge tested code to main
- Use branches for development
- Tag stable releases

### 2. Update Dependencies Regularly

```bash
npm update
npm audit fix
git commit -am "Update dependencies"
git push
```

### 3. Version Your Releases

```bash
# Create tagged releases
git tag -a v1.1.0 -m "Add new features"
git push origin v1.1.0

# Users can then use specific versions
npx create-next-app@latest my-app -e yourusername/template/tree/v1.1.0
```

### 4. Document Breaking Changes

- Update CHANGELOG.md
- Use semantic versioning
- Provide migration guides

## 🆘 Troubleshooting

### "Repository not found"

- Ensure repository is public
- Check repository name spelling
- Verify GitHub username

### "Template download failed"

- Check internet connection
- Try with full GitHub URL
- Verify repository accessibility

### "Dependencies installation failed"

- Check Node.js version (20+)
- Clear npm cache: `npm cache clean --force`
- Try manual install: `npm install`

### Init script doesn't run

```bash
# Make executable
chmod +x scripts/init-project.sh

# Run with bash explicitly
bash scripts/init-project.sh
```

## 📊 Usage Statistics

Track template usage with:

- GitHub repository insights
- Clone statistics
- Star count
- Fork count

## 🎉 Promoting Your Template

### 1. Add Badge to README

```markdown
[![Use this template](https://img.shields.io/badge/use%20this-template-blue?logo=github)](https://github.com/yourusername/your-template-repo/generate)

[![Create with create-next-app](https://img.shields.io/badge/create--next--app-ready-success?logo=next.js)](https://github.com/yourusername/your-template-repo)
```

### 2. Share on Social Media

- Twitter/X with #nextjs #template
- Reddit r/nextjs
- Dev.to article
- LinkedIn post

### 3. Add to Lists

- Awesome Next.js
- Next.js examples
- Template collections

### 4. Create Demo Video

Show:

1. Creating project with create-next-app
2. Running init script
3. Starting development
4. Building a feature

## 📞 Quick Reference

### Create New Project

```bash
npx create-next-app@latest PROJECT_NAME -e GITHUB_URL
```

### Your Template Command

```bash
npx create-next-app@latest my-app -e https://github.com/yourusername/your-template-repo
```

### With Specific Version

```bash
npx create-next-app@latest my-app -e https://github.com/yourusername/your-template-repo/tree/v1.0.0
```

### Full Setup

```bash
npx create-next-app@latest my-app -e yourusername/template && cd my-app && ./scripts/init-project.sh && npm run dev
```

## 🎊 Success!

Your template is now:

- ✅ Usable with create-next-app
- ✅ Easy to discover and use
- ✅ Professional and polished
- ✅ Ready for the community

**Share your template and help other developers build faster!** 🚀

---

## 📚 Additional Resources

- [Next.js create-next-app docs](https://nextjs.org/docs/app/api-reference/cli/create-next-app)
- [GitHub Template Repositories](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository)
- [npm create-next-app](https://www.npmjs.com/package/create-next-app)

---

**Now anyone can use your template with a single command!** ✨

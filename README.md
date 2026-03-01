# Broken Semantics

Personal blog built with Hugo and the Stack theme, deployed to AWS S3 + CloudFront.

**Live site:** https://joaomaia.dev/

## Prerequisites

- Hugo (extended version with deploy support)
- AWS CLI configured with credentials
- Git (for theme submodule management)

## Initial Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd broken-semantics
   ```

2. **Initialize the theme submodule**
   ```bash
   git submodule update --init --recursive
   ```

3. **Configure AWS credentials**

   Create an IAM user with S3 and CloudFront permissions, then configure:
   ```bash
   aws configure --profile hugo-deploy
   ```

   Enter your access key ID, secret key, and set region to `sa-east-1`.

## Creating New Articles

1. **Create a new post**
   ```bash
   hugo new posts/my-article-name.md
   ```

   This creates a new file in `content/posts/` with front matter template.

2. **Edit the article**

   Open `content/posts/my-article-name.md` and edit:

   ```markdown
   +++
   title = 'My Article Title'
   date = 2024-05-04T13:52:19-03:00
   draft = false  # Change to false when ready to publish
   +++

   Your content here...
   ```

3. **Preview locally**
   ```bash
   # Include drafts
   hugo server -D

   # Preview only published posts
   hugo server
   ```

   Visit http://localhost:1313

4. **Publish the article**

   Set `draft = false` in the article's front matter, then commit:
   ```bash
   git add content/posts/my-article-name.md
   git commit -m "post: add new article about X"
   git push
   ```

## Deploying to Production

1. **Build the site**
   ```bash
   hugo
   ```

   This generates static files in the `public/` directory.

2. **Deploy to S3**
   ```bash
   AWS_PROFILE=hugo-deploy hugo deploy --target production
   ```

   This will:
   - Upload new/changed files to S3 bucket `broken-semantics`
   - Invalidate CloudFront CDN cache
   - Make the site live at https://joaomaia.dev/

3. **Dry run (preview changes)**
   ```bash
   AWS_PROFILE=hugo-deploy hugo deploy --target production --dryRun
   ```

## Quick Workflow

```bash
# Create new post
hugo new posts/my-new-post.md

# Edit the file, set draft = false when ready

# Preview locally
hugo server -D

# Build and deploy
hugo
AWS_PROFILE=hugo-deploy hugo deploy --target production

# Commit to git
git add .
git commit -m "post: add new post about X"
git push
```

## Configuration

- Main config: `hugo.toml`
- Detailed settings: `config/_default/*.toml`
- Theme: `themes/hugo-theme-stack` (git submodule)
- Content: `content/posts/`
- Static files: `static/`
- Generated site: `public/` (not committed to git)

## Deployment Configuration

The site deploys to:
- **S3 Bucket:** `broken-semantics` (region: sa-east-1)
- **CloudFront Distribution:** E1IQ2IVCHRKLEW
- **Domain:** joaomaia.dev

Configuration is in `hugo.toml` under `[deployment]`.

## Troubleshooting

**Theme not found:**
```bash
git submodule update --init --recursive
```

**AWS credentials error:**
```bash
# Verify credentials work
aws s3 ls --profile hugo-deploy

# Re-configure if needed
aws configure --profile hugo-deploy
```

**Hugo not found:**
```bash
brew install hugo
```

For more details, see [CLAUDE.md](CLAUDE.md).

# Broken Semantics

Personal blog built with Hugo and the Stack theme, deployed to AWS S3 + CloudFront.

**Live site:** https://joaomaia.dev/

## Prerequisites

- Hugo extended+withdeploy (v0.133.0+)
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

## Creating New Articles

1. **Create a new post**
   ```bash
   hugo new posts/my-article-name.md
   ```

2. **Edit the article** — open `content/posts/my-article-name.md` and set `draft = false` when ready to publish.

3. **Preview locally**
   ```bash
   hugo server -D
   ```
   Visit http://localhost:1313

4. **Publish** — set `draft = false`, commit, and push to `main`. CI will build and deploy automatically.

## CI/CD Deployment

Pushing to `main` triggers the [GitHub Actions workflow](.github/workflows/deploy.yml), which:
1. Builds the site with `hugo --minify`
2. Syncs to S3 and invalidates CloudFront with `hugo deploy --target production`

### Required GitHub configuration

**Secrets** (Settings → Secrets and variables → Actions → Secrets):

| Secret | Description |
|---|---|
| `AWS_ROLE_ARN` | ARN of the IAM role assumed via OIDC |
| `GA_MEASUREMENT_ID` | Google Analytics measurement ID (e.g. `G-XXXXXXXXXX`) |

**Variables** (Settings → Secrets and variables → Actions → Variables):

| Variable | Description |
|---|---|
| `DEPLOY_S3_BUCKET` | S3 bucket full URL |
| `DEPLOY_CF_DISTRIBUTION_ID` | CloudFront distribution ID |

### IAM Role setup

The workflow authenticates via OIDC — no long-lived access keys needed. The IAM role must:
- Trust `token.actions.githubusercontent.com` for this repository's `main` branch
- Allow `s3:PutObject`, `s3:DeleteObject`, `s3:ListBucket`, `s3:GetObject` on the S3 bucket
- Allow `cloudfront:CreateInvalidation` on the distribution

See [AWS OIDC documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_create_oidc.html) for setup steps.

## Local Deployment

To deploy manually, substitute the placeholders in `hugo.toml` and run:

```bash
S3_BUCKET=your-bucket DEPLOY_CF_DISTRIBUTION_ID=your-cf-id \
  sed -i "s|DEPLOY_S3_URL|${DEPLOY_S3_URL}|g; s|DEPLOY_CF_DISTRIBUTION_ID|${DEPLOY_CF_DISTRIBUTION_ID}|g" hugo.toml

AWS_PROFILE=hugo-deploy hugo deploy --target production
```

> **Note:** Remember to revert `hugo.toml` after a local deploy (`git checkout hugo.toml`).

## Configuration

- Main config: `hugo.toml` + `config/_default/*.toml`
- Theme: `themes/hugo-theme-stack` (git submodule)
- Content: `content/posts/`
- Generated site: `public/` (not committed)

## Troubleshooting

**Theme not found:**
```bash
git submodule update --init --recursive
```

**Hugo not found or wrong version:**
```bash
brew install hugo        # install
brew upgrade hugo        # upgrade
hugo version             # verify: must include +extended+withdeploy
```

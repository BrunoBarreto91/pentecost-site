# Deployment Guide — GitHub → AWS Amplify

This guide explains how to deploy the portfolio site using AWS Amplify with GitHub as the source.

## Prerequisites

- AWS Account with Amplify access
- GitHub repository created and pushed
- AWS CLI configured (optional, for manual operations)

## Initial Setup: Connect GitHub to Amplify

### 1. Access AWS Amplify Console

1. Log in to [AWS Console](https://console.aws.amazon.com/)
2. Navigate to **AWS Amplify**
3. Click **"New app"** → **"Host web app"**

### 2. Connect GitHub Repository

1. Select **GitHub** as the source
2. Authorize AWS Amplify to access your GitHub account
3. Select repository: `BrunoBarreto91/pentecost-site`
4. Select branch: `main`
5. Click **"Next"**

### 3. Configure Build Settings

Since this is a static site with no build step, use the default configuration:

```yaml
version: 1
frontend:
  phases:
    build:
      commands: []
  artifacts:
    baseDirectory: /
    files:
      - '**/*'
  cache:
    paths: []
```

Click **"Next"** → **"Save and deploy"**

### 4. Deployment Complete

Amplify will:
- Clone the repository
- Deploy all files to S3
- Configure CloudFront distribution
- Provide a deployment URL (e.g., `https://main.d224tz0vfoxquk.amplifyapp.com/`)

## Deployment Flow

```
Developer → git push origin main → GitHub → Amplify Webhook → Build → Deploy → CloudFront Invalidation → Live Site
```

### Automatic Deployment

Every push to the `main` branch triggers:

1. **Webhook notification** from GitHub to Amplify
2. **Build phase** (instant for static sites)
3. **Deploy phase** (files uploaded to S3)
4. **CloudFront cache invalidation** (CDN refresh)
5. **Site live** (typically < 2 minutes)

## Environment Variables

This static site requires no environment variables. If you need to add any in the future:

1. Go to **Amplify Console** → Your app
2. Click **"Environment variables"** in the left menu
3. Add key-value pairs
4. Redeploy

## Custom Domain (Future)

When you acquire a custom domain:

### 1. Add Domain in Amplify

1. Go to **Amplify Console** → Your app
2. Click **"Domain management"**
3. Click **"Add domain"**
4. Enter your domain (e.g., `brunobarreto.dev`)

### 2. Configure DNS

Amplify will provide DNS records. Add them to your domain registrar:

```
Type: CNAME
Name: www
Value: [provided by Amplify]

Type: A
Name: @
Value: [provided by Amplify]
```

### 3. SSL Certificate

Amplify automatically provisions an SSL certificate via AWS Certificate Manager (ACM). This process takes 5-10 minutes.

## Monitoring & Logs

### View Deployment Logs

1. Go to **Amplify Console** → Your app
2. Click on a deployment in the list
3. View build logs and deployment status

### Access Logs

CloudFront access logs can be enabled:

1. Go to **CloudFront Console**
2. Select your distribution
3. Edit **"Logging"** settings
4. Specify an S3 bucket for logs

## Rollback

To rollback to a previous version:

1. Go to **Amplify Console** → Your app
2. Find the previous successful deployment
3. Click **"Redeploy this version"**

Or use Git:

```bash
# Revert to previous commit
git revert HEAD
git push origin main

# Or reset to specific commit
git reset --hard <commit-hash>
git push origin main --force
```

## Cost Optimization

### Current Setup

- **Amplify Hosting:** Free tier covers most personal sites
- **CloudFront:** Pay-as-you-go (minimal for low traffic)
- **S3 Storage:** ~$0.023/GB/month
- **Estimated monthly cost:** < $1 for typical portfolio traffic

### Optimization Tips

1. **Compress images:** Use WebP format where possible
2. **Lazy load videos:** Use `preload="none"` attribute
3. **Cache headers:** Set long cache times for static assets
4. **CloudFront:** Leverage edge caching to reduce origin requests

## Troubleshooting

### Deployment Fails

**Check build logs:**
1. Amplify Console → Your app → Failed deployment
2. Review error messages in build logs

**Common issues:**
- Missing files in repository
- Incorrect file paths (case-sensitive)
- Large files exceeding limits

### Site Not Updating

**CloudFront cache:**
1. Go to **CloudFront Console**
2. Select your distribution
3. Create invalidation for `/*`

Or wait for TTL expiration (typically 24 hours).

### 404 Errors

**Check file paths:**
- Ensure all links use relative paths (`./` prefix)
- Verify file names match exactly (case-sensitive)

## Manual Deployment (Alternative)

If you need to deploy manually without GitHub:

```bash
# Install AWS CLI
aws configure

# Sync files to S3
aws s3 sync . s3://your-bucket-name --exclude ".git/*" --exclude "node_modules/*"

# Invalidate CloudFront cache
aws cloudfront create-invalidation --distribution-id YOUR_DIST_ID --paths "/*"
```

## Security

### Best Practices

1. **Never commit secrets:** Use `.gitignore` for sensitive files
2. **Enable HTTPS:** Amplify provides SSL by default
3. **Restrict S3 access:** Amplify manages bucket permissions automatically
4. **Monitor access:** Enable CloudFront logging for security audits

## Support

For issues or questions:

- **AWS Amplify Docs:** [docs.aws.amazon.com/amplify](https://docs.aws.amazon.com/amplify/)
- **GitHub Issues:** [github.com/BrunoBarreto91/pentecost-site/issues](https://github.com/BrunoBarreto91/pentecost-site/issues)
- **Email:** brunocesar1291@gmail.com

---

**Last updated:** April 2026

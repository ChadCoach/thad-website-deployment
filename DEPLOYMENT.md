# Thad Website Deployment Guide

## 1. Introduction

### 1.1 Purpose & Scope
This guide outlines the deployment process for thethad.de website, built with Next.js and shadcn/ui components, to be deployed on Vercel with a custom domain.

### 1.2 Target Environment
- Production deployment on Vercel
- Custom domain: thethad.de
- Next.js 14 optimization settings

## 2. Prerequisites

### 2.1 Required Accounts
1. GitHub account (already set up at github.com/thad0thad)
2. Vercel account (sign up at vercel.com)
3. Domain registrar access (for thethad.de)

### 2.2 Local Development Setup
```bash
# Install required tools
npm install -g vercel    # Vercel CLI
```

## 3. Implementation Steps

### 3.1 Project Preparation
1. Initialize Git repository:
```bash
git init
git add .
git commit -m "Initial commit"
```

2. Connect to GitHub repository:
```bash
git remote add origin https://github.com/thad0thad/thethad-website.git
git push -u origin main
```

3. Verify package.json contains:
```json
{
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  }
}
```

### 3.2 Environment Setup
1. Create `.env.local` file:
```
NEXT_PUBLIC_SITE_URL=https://thethad.de
```

2. Create `.gitignore`:
```
node_modules
.next
.env.local
.env.development.local
.env.test.local
.env.production.local
```

### 3.3 Vercel Deployment

1. Log into Vercel:
```bash
vercel login
```

2. Initial deployment:
```bash
vercel
```

3. For subsequent deployments:
```bash
vercel --prod
```

### 3.4 Domain Configuration

1. In Vercel Dashboard:
   - Go to Project Settings
   - Navigate to Domains
   - Add thethad.de

2. At Domain Registrar:
   - Add DNS records:
```
Type    Name    Value
A       @       76.76.21.21
CNAME   www     cname.vercel-dns.com
```

## 4. File Structure Updates

```
thethad-website/
├── .env.local
├── .gitignore
├── next.config.js
├── package.json
├── app/
│   ├── layout.tsx
│   └── page.tsx
└── public/
    └── robots.txt
```

## 5. Configuration Files

### 5.1 next.config.js
```javascript
/** @type {import('next').NextConfig} */
const nextConfig = {
  output: 'standalone',
  images: {
    domains: ['your-image-domains.com'],
  },
}

module.exports = nextConfig
```

### 5.2 robots.txt
```txt
User-agent: *
Allow: /
Sitemap: https://thethad.de/sitemap.xml
```

## 6. Post-Deployment Checklist

1. Verify production build:
   - Check https://thethad.de
   - Test all navigation links
   - Verify shadcn/ui components
   - Check mobile responsiveness

2. Performance validation:
   - Run Lighthouse audit
   - Check Core Web Vitals
   - Verify HTTPS configuration

3. Domain verification:
   - SSL certificate active
   - Domain resolves correctly
   - WWW redirect working

## 7. Ongoing Maintenance

### 7.1 Deployment Process
```bash
# For each update:
git add .
git commit -m "Update description"
git push origin main    # Vercel auto-deploys
```

### 7.2 Monitoring
- Set up Vercel Analytics (optional)
- Configure status notifications
- Monitor build logs

## 8. Troubleshooting Guide

Common issues and solutions:

1. Build failures:
   - Check build logs in Vercel dashboard
   - Verify all dependencies are properly installed
   - Check environment variables are set

2. Domain issues:
   - DNS propagation can take up to 48 hours
   - Verify DNS records match Vercel requirements
   - Check SSL certificate status

## 9. Commands Reference

```bash
# Development
npm run dev

# Production build test
npm run build
npm start

# Deploy
vercel
vercel --prod

# Domain configuration
vercel domains add thethad.de
```

## 10. Support and Resources

- Vercel Documentation: https://vercel.com/docs
- Next.js Documentation: https://nextjs.org/docs
- shadcn/ui Documentation: https://ui.shadcn.com
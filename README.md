# Codify - Landing Page

> All-in-One COD Suite for Shopify

## 🚀 Project Structure

```
codify/
├── index.html                    # Main landing page
├── privacy-policy.html           # Privacy policy page
├── terms-of-service.html         # Terms of service page
├── contact-support.html          # Contact support page
├── assets/
│   ├── images/                   # All image assets
│   │   ├── logo.png
│   │   ├── blacklist.png
│   │   ├── buy-button.png
│   │   ├── custom-form.png
│   │   ├── data-validation.png
│   │   ├── fraud-detection.png
│   │   ├── hide-add-to-card.png
│   │   ├── quantity-offer.png
│   │   └── upsell.png
│   └── videos/                   # Video assets
│       └── codify-in-action.mp4
└── docs/
    └── GOOGLE_SHEETS_SETUP.md    # Setup documentation

```

## 📋 Features

- **Static HTML Website** - No build process required
- **Responsive Design** - Mobile-friendly with Tailwind CSS
- **Google Sheets Integration** - Order form connected to Google Sheets
- **SEO Optimized** - Proper meta tags and semantic HTML
- **Fast Loading** - Optimized assets and clean code

## 🌐 Deployment Options

### Option 1: Static Hosting (Recommended)

Deploy to any static hosting service:

- **Netlify**: Drag and drop the entire `codify` folder to [Netlify Drop](https://app.netlify.com/drop)
- **Vercel**: Run `npx vercel` in the project directory
- **GitHub Pages**: Push to GitHub and enable Pages in repository settings
- **Cloudflare Pages**: Connect your GitHub repo or upload files directly

### Option 2: Traditional Web Hosting

1. Upload all files via FTP/SFTP to your web server
2. Ensure `index.html` is in the root directory
3. Set up SSL certificate (most hosts provide free Let's Encrypt)

### Option 3: CDN Deployment

For maximum performance:

1. Upload to origin server
2. Configure CDN (Cloudflare, AWS CloudFront, etc.)
3. Set cache rules for assets/*

## 🔧 Configuration

### Google Sheets Integration

1. Follow instructions in `docs/GOOGLE_SHEETS_SETUP.md`
2. Update the `GOOGLE_SHEETS_URL` in `index.html` (line 3270)

### Custom Domain

1. Add your domain in hosting provider settings
2. Update DNS records (A or CNAME)
3. Enable SSL/HTTPS

## 📝 Customization

### Updating Content

- **Main Page**: Edit `index.html`
- **Pricing**: Lines 2835-2941 in `index.html`
- **Images**: Replace files in `assets/images/`
- **Video**: Replace `assets/videos/codify-in-action.mp4`

### Styling

All styling is inline using Tailwind CSS classes. To modify:

1. Find the section you want to change in `index.html`
2. Update the class names or content
3. Save and refresh

## 🎯 SEO Checklist

- [x] Unique title and meta description
- [x] Proper heading hierarchy (H1, H2, H3)
- [x] Alt text for all images
- [x] Semantic HTML structure
- [x] Mobile-responsive design
- [ ] Submit sitemap to search engines
- [ ] Add Google Analytics (optional)
- [ ] Add favicon

## 🔒 Security

- Form submissions go through Google Apps Script
- No sensitive data stored client-side
- HTTPS recommended for production

## 📊 Analytics (Optional)

To add Google Analytics:

1. Get your tracking ID from Google Analytics
2. Add the tracking script before `</head>` in all HTML files
3. Test in preview mode before deploying

## 🐛 Troubleshooting

**Images not loading?**
- Check file paths are correct
- Verify all files are uploaded to server
- Clear browser cache

**Form not submitting?**
- Verify Google Sheets URL is correct
- Check Google Apps Script deployment is active
- Review browser console for errors

**Video not playing?**
- Ensure MP4 format is supported
- Check file size isn't too large
- Verify correct MIME type on server

## 📦 File Sizes

Keep assets optimized:
- Images: Use WebP or optimized PNG/JPEG
- Videos: Compress to reasonable bitrate
- Target total page size: < 3MB

## 🚦 Performance Tips

1. **Enable Caching**: Set long cache times for assets
2. **Compress Assets**: Use image compression tools
3. **Lazy Loading**: Video loads on demand
4. **CDN**: Use a CDN for global performance

## 📞 Support

For issues or questions:
- Check documentation in `docs/`
- Review code comments in HTML files
- Contact via the contact-support.html form

## 📄 License

All rights reserved - Codify App © 2025

---

**Ready to deploy?** Choose a hosting option above and upload your files!

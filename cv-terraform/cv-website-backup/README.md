# Modular CV Website - Indranil Biswas

Professional, modular CV website with separate CSS and JavaScript files. Features a modern dark theme with profile photo integration.

## ✨ Features

### Design
- ✅ **Modern Dark Theme**: Professional cyan/purple color scheme
- ✅ **Profile Photo Integration**: Large photo in hero, small logo in navbar
- ✅ **Modular Architecture**: Separate HTML, CSS, and JavaScript files
- ✅ **Fully Responsive**: Perfect on all devices
- ✅ **Smooth Animations**: Scroll effects and transitions
- ✅ **Mobile Menu**: Hamburger menu for mobile devices

### Technical
- ✅ **Clean Code Structure**: Easy to maintain and update
- ✅ **No Dependencies**: Pure HTML/CSS/JavaScript
- ✅ **Fast Loading**: Optimized for performance
- ✅ **SEO Friendly**: Proper meta tags and structure
- ✅ **Accessible**: Keyboard navigation support

## 📁 Project Structure

```
modular-cv-website/
│
├── index.html              # Main HTML file
│
├── css/
│   └── styles.css         # All styles (organized with comments)
│
├── js/
│   └── main.js            # All JavaScript functionality
│
├── images/
│   ├── profile.jpg        # Your profile photo (500x500)
│   └── profile-logo.png   # Logo for navbar (200x200)
│
├── README.md              # This file
├── IMAGE_GUIDE.md         # Complete image preparation guide
└── DEPLOYMENT.md          # Deployment instructions
```

## 🚀 Quick Start

### 1. Add Your Images

#### Prepare your profile photo:
```bash
# Create images folder
mkdir images

# Add your photos
# - profile.jpg (500x500 pixels) - Main profile photo
# - profile-logo.png (200x200 pixels) - Navbar logo
```

**📖 See [IMAGE_GUIDE.md](IMAGE_GUIDE.md) for detailed instructions on creating these images**

### 2. Test Locally

```bash
# Option 1: Open directly in browser
open index.html

# Option 2: Use Python HTTP server
python3 -m http.server 8000
# Visit http://localhost:8000

# Option 3: Use Node.js http-server
npx http-server -p 8000
```

### 3. Customize Content

Edit `index.html` to update:
- Personal information
- Contact links
- Work experience
- Skills
- Certifications

### 4. Customize Styling (Optional)

Edit `css/styles.css` - CSS variables at the top:

```css
:root {
    --primary: #00d4ff;      /* Change primary color */
    --secondary: #7c3aed;    /* Change secondary color */
    --bg-dark: #0a0e27;      /* Change background */
}
```

## 🎨 Customization Guide

### Change Colors

Open `css/styles.css` and modify CSS variables (lines 6-18):

```css
:root {
    --bg-dark: #0a0e27;           /* Main background */
    --bg-card: #1a1f3a;           /* Card background */
    --primary: #00d4ff;           /* Primary accent (cyan) */
    --secondary: #7c3aed;         /* Secondary accent (purple) */
    --accent: #f59e0b;            /* Accent color (orange) */
    --text-primary: #ffffff;      /* Main text */
    --text-secondary: #94a3b8;    /* Secondary text */
    --text-muted: #64748b;        /* Muted text */
}
```

### Update Contact Information

Edit `index.html`, find the social links section:

```html
<div class="social-links">
    <a href="mailto:your-email@example.com">📧</a>
    <a href="https://linkedin.com/in/yourprofile">💼</a>
    <a href="https://github.com/yourusername">🐙</a>
</div>
```

### Add New Sections

Copy the section structure from existing sections in `index.html`:

```html
<section id="new-section" class="container">
    <div class="section">
        <div class="section-header">
            <div class="section-tag">Section Tag</div>
            <h2 class="section-title">Section Title</h2>
        </div>
        <!-- Your content here -->
    </div>
</section>
```

## 📤 Deployment Options

### Option 1: AWS S3 (Static Website Hosting)

```bash
# Upload all files
aws s3 sync . s3://your-bucket-name/ \
  --exclude ".git/*" \
  --exclude "*.md" \
  --exclude ".DS_Store"

# Or use the existing bucket
aws s3 sync . s3://indranilbiswas/ \
  --exclude ".git/*" \
  --exclude "*.md"
```

### Option 2: AWS S3 + CloudFront (Recommended)

```bash
# Use the Terraform infrastructure package
cd cv-website-terraform

# Copy your modular CV to example-site
cp -r ../modular-cv-website/* ./example-site/

# Deploy with Terraform
terraform apply

# Upload to S3
aws s3 sync example-site/ s3://$(terraform output -raw s3_bucket_name)/

# Invalidate CloudFront cache
aws cloudfront create-invalidation \
  --distribution-id $(terraform output -raw cloudfront_distribution_id) \
  --paths "/*"
```

### Option 3: GitHub Pages

```bash
# Push to GitHub repository
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/yourusername/cv-website.git
git push -u origin main

# Enable GitHub Pages in repository settings
# Your site will be at: https://yourusername.github.io/cv-website
```

### Option 4: Netlify

```bash
# Install Netlify CLI
npm install -g netlify-cli

# Deploy
netlify deploy --prod
```

## 🔧 File Descriptions

### HTML (`index.html`)
- Semantic HTML5 structure
- Proper heading hierarchy
- Meta tags for SEO
- Accessibility attributes
- Modular section design

### CSS (`css/styles.css`)
```
├── CSS Variables (easy theming)
├── Base Styles
├── Navigation
├── Hero Section with Profile Image
├── Cards and Sections
├── Timeline
├── Certifications
├── Footer
├── Animations
└── Responsive Design (mobile-first)
```

### JavaScript (`js/main.js`)
```
├── Smooth Scroll Navigation
├── Mobile Menu Toggle
├── Scroll Animations
├── Active Navigation Highlighting
├── Navbar Effects
├── Image Error Handling
├── Parallax Effects
├── Keyboard Navigation
└── Utility Functions
```

## 📱 Responsive Breakpoints

The website is fully responsive with these breakpoints:

- **Desktop**: > 968px
- **Tablet**: 768px - 968px
- **Mobile**: < 768px
- **Small Mobile**: < 480px

## 🎯 Features Breakdown

### Navigation
- Sticky navbar with blur effect
- Smooth scrolling to sections
- Active link highlighting
- Mobile hamburger menu
- Keyboard shortcuts (H for home, ESC to close menu)

### Hero Section
- Profile photo on left (250px)
- Content on right
- Pulsing ring animation around photo
- Gradient text for name
- Call-to-action buttons

### Experience Timeline
- Visual timeline with connection line
- Hover effects on items
- Progressive display animation
- Clean card-based design

### Skills Section
- Categorized skills (Networking, Cloud, DevOps, Systems)
- Icon-based headers
- Hover effects
- Grid layout

### Certifications
- Badge-style cards
- Color-coded status (completed/in-progress)
- Gradient top border
- Click to copy certification name

## ⚡ Performance

### Optimization Features
- Minimal CSS (no frameworks)
- No external dependencies
- Lazy loading for images (built-in)
- Debounced scroll events
- Optimized animations
- Gzip-friendly file structure

### Expected Performance
- **Load Time**: < 1 second
- **Lighthouse Score**: 95+
- **First Contentful Paint**: < 0.5s
- **Time to Interactive**: < 1s

## 🔒 Security

- No inline styles or scripts
- No external CDN dependencies
- No tracking scripts (privacy-first)
- HTTPS ready
- No form submissions (static site)

## 🌐 Browser Support

- ✅ Chrome 90+
- ✅ Firefox 88+
- ✅ Safari 14+
- ✅ Edge 90+
- ✅ Mobile browsers (iOS Safari, Chrome Mobile)

## 🐛 Troubleshooting

### Images not loading?

1. Check file paths in `index.html`:
```html
<img src="images/profile.jpg" alt="...">
<img src="images/profile-logo.png" alt="...">
```

2. Verify images exist in `images/` folder
3. Check browser console (F12) for errors
4. Ensure file names match exactly (case-sensitive)

### Styles not applying?

1. Check CSS file path in `index.html`:
```html
<link rel="stylesheet" href="css/styles.css">
```

2. Clear browser cache (Ctrl+Shift+R or Cmd+Shift+R)
3. Check for CSS syntax errors

### JavaScript not working?

1. Check JS file path in `index.html`:
```html
<script src="js/main.js"></script>
```

2. Open browser console (F12) for errors
3. Ensure script is at bottom of `<body>` tag

### Mobile menu not working?

1. Ensure screen width is < 768px
2. Check JavaScript console for errors
3. Try clearing cache

## 📝 Maintenance

### Updating Content

1. **Work Experience**: Edit timeline items in `index.html`
2. **Skills**: Modify skill lists in skills section
3. **Certifications**: Add/update cert badges
4. **Contact Info**: Update social links in footer

### Updating Styles

1. **Colors**: Change CSS variables in `css/styles.css`
2. **Layout**: Modify grid templates
3. **Animations**: Adjust keyframes and transitions

### Adding Features

1. Create new section in `index.html`
2. Style it in `css/styles.css`
3. Add interactivity in `js/main.js`

## 💡 Tips

1. **Keep It Simple**: Don't over-customize - professional simplicity works best
2. **Test Mobile First**: Most visitors view on mobile
3. **Optimize Images**: Use compressed images (<500KB total)
4. **Update Regularly**: Keep content fresh (every 3-6 months)
5. **Backup**: Version control with Git
6. **Analytics**: Add Google Analytics if needed

## 📦 What's Included

- ✅ Complete HTML structure
- ✅ Modular CSS (organized with comments)
- ✅ Interactive JavaScript
- ✅ Image preparation guide
- ✅ Deployment instructions
- ✅ Customization examples
- ✅ Responsive design
- ✅ Professional styling

## 🆘 Need Help?

1. **Image Preparation**: See [IMAGE_GUIDE.md](IMAGE_GUIDE.md)
2. **Deployment**: See [DEPLOYMENT.md](DEPLOYMENT.md)
3. **CSS**: Check inline comments in `css/styles.css`
4. **JavaScript**: Check function comments in `js/main.js`

## 📄 License

This CV website template is provided for personal use. Feel free to customize and deploy!

## 🎓 Learning Resources

- **HTML**: https://developer.mozilla.org/en-US/docs/Web/HTML
- **CSS**: https://developer.mozilla.org/en-US/docs/Web/CSS
- **JavaScript**: https://developer.mozilla.org/en-US/docs/Web/JavaScript
- **Responsive Design**: https://web.dev/responsive-web-design-basics/

---

**Version**: 2.0 Modular  
**Last Updated**: January 2026  
**Author**: Indranil Biswas  
**Built With**: HTML5, CSS3, JavaScript ES6

**Ready to deploy!** 🚀 Follow the deployment guide to get your CV online.

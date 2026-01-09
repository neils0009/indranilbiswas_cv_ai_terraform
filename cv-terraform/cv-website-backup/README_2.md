# Images Folder

This folder should contain your profile images for the CV website.

## Required Images

### 1. profile.jpg
- **Purpose**: Main profile photo in hero section
- **Size**: 500x500 pixels
- **Format**: JPG or PNG
- **File Size**: Under 200KB (optimized)
- **Description**: Your professional headshot

### 2. profile-logo.png
- **Purpose**: Small logo in navigation bar and favicon
- **Size**: 200x200 pixels
- **Format**: PNG (with or without transparency)
- **File Size**: Under 50KB
- **Description**: Smaller version of profile photo or custom logo

## Quick Setup

### Option 1: Use Your Own Photos

```bash
# Copy your photos to this folder
cp /path/to/your/photo.jpg profile.jpg
cp /path/to/your/logo.png profile-logo.png
```

### Option 2: Create from Single Photo

If you only have one photo, create both versions:

```bash
# Using ImageMagick (install first)
# Create main profile (500x500)
convert your-photo.jpg -resize 500x500^ -gravity center -extent 500x500 profile.jpg

# Create logo (200x200)
convert your-photo.jpg -resize 200x200^ -gravity center -extent 200x200 profile-logo.png
```

### Option 3: Online Tools

1. Go to https://www.photopea.com/
2. Upload your photo
3. Resize to 500x500 and save as `profile.jpg`
4. Resize to 200x200 and save as `profile-logo.png`

## 📖 Detailed Instructions

See the **IMAGE_GUIDE.md** in the project root for complete instructions on:
- Creating professional photos
- Image editing tools
- Optimizing file sizes
- Creating circular logos
- And much more!

## ✅ Checklist

Before deployment, ensure:
- [ ] `profile.jpg` exists (500x500px)
- [ ] `profile-logo.png` exists (200x200px)
- [ ] Both files are under 500KB combined
- [ ] Images are professional quality
- [ ] Images are properly cropped/centered
- [ ] Tested in website locally

## 🎨 Image Specifications

### profile.jpg
```
Dimensions: 500 x 500 pixels
Format: JPEG
Quality: 85-90%
Color Space: sRGB
Max File Size: 200 KB
Use: Hero section, large display
```

### profile-logo.png
```
Dimensions: 200 x 200 pixels
Format: PNG
Quality: Best
Transparency: Optional
Max File Size: 50 KB
Use: Navbar, favicon, mobile
```

## 🚀 After Adding Images

1. Test locally:
   ```bash
   open ../index.html
   ```

2. Verify images load correctly
3. Check appearance on mobile (Chrome DevTools)
4. Deploy to S3:
   ```bash
   aws s3 sync . s3://your-bucket/images/
   ```

## 💡 Tips

- Use high-quality original photos
- Ensure good lighting
- Professional background
- Clear face visibility
- Optimize before uploading
- Keep backups of originals

## 🆘 Need Help?

See **IMAGE_GUIDE.md** for:
- Step-by-step photo editing
- Free online tools
- Command-line options
- Troubleshooting
- Best practices

---

**Ready?** Add your photos and test the website! 🎉

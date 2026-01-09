# Terraform Fixes - Quick Update

Modified files only - replace these in your existing `cv-website-terraform` directory.

## 🔧 What Was Fixed

### 1. S3 Lifecycle Configuration (Lines 57, 97)
**Issue:** Warning about missing filter attribute  
**Fix:** Added `filter {}` to lifecycle rules

### 2. CloudFront Response Headers Policy (Lines 183-235)
**Issue:** CSP header in wrong block causing deployment error  
**Fix:** Moved `Content-Security-Policy` from `custom_headers_config` to `security_headers_config`

### 3. New Documentation
**Added:** TROUBLESHOOTING.md with solutions for common issues

## 📦 Files Included

```
terraform-fixes/
├── main.tf                # Fixed Terraform configuration
├── TROUBLESHOOTING.md     # New troubleshooting guide
└── README.md              # This file
```

## 🚀 How to Apply These Fixes

### Option 1: Replace Files (Recommended)

```bash
# Navigate to your terraform directory
cd cv-website-terraform

# Backup current files
cp main.tf main.tf.backup

# Replace with fixed versions
cp /path/to/terraform-fixes/main.tf .
cp /path/to/terraform-fixes/TROUBLESHOOTING.md .

# Verify changes
terraform validate

# Deploy
terraform apply
```

### Option 2: Manual Update

If you've made custom changes to `main.tf`, apply these specific changes:

#### Fix 1: S3 Lifecycle - Line 57
```hcl
# Add this line:
resource "aws_s3_bucket_lifecycle_configuration" "website" {
  bucket = aws_s3_bucket.website.id

  rule {
    id     = "cleanup-old-versions"
    status = "Enabled"
    
    filter {}  # ← ADD THIS LINE
    
    noncurrent_version_expiration {
      noncurrent_days = 90
    }
    # ...
  }
}
```

#### Fix 2: S3 Lifecycle (Logs) - Line 97
```hcl
# Add this line:
resource "aws_s3_bucket_lifecycle_configuration" "logs" {
  # ...
  rule {
    id     = "expire-logs"
    status = "Enabled"
    
    filter {}  # ← ADD THIS LINE
    
    expiration {
      days = 90
    }
  }
}
```

#### Fix 3: CloudFront Headers - Lines 183-235
```hcl
resource "aws_cloudfront_response_headers_policy" "security_headers" {
  # ...
  
  security_headers_config {
    # ... existing headers ...
    
    # ADD THIS BLOCK (move from custom_headers):
    content_security_policy {
      content_security_policy = "default-src 'self'; img-src 'self' data: https:; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'; font-src 'self' data:; object-src 'none'; base-uri 'self'; form-action 'self'; frame-ancestors 'none';"
      override                = true
    }
  }

  custom_headers_config {
    # REMOVE Content-Security-Policy from here
    
    # KEEP only this:
    items {
      header   = "Permissions-Policy"
      override = true
      value    = "geolocation=(), microphone=(), camera=()"
    }
  }
}
```

## ✅ Verification

After applying fixes:

```bash
# Validate configuration
terraform validate
# Expected: Success! The configuration is valid.

# Check plan
terraform plan
# Expected: No warnings, clean plan

# Deploy
terraform apply
```

## 🎯 What These Fixes Enable

- ✅ No Terraform warnings during `plan` or `apply`
- ✅ CloudFront security headers deploy correctly
- ✅ S3 lifecycle policies work as expected
- ✅ Proper CSP header configuration
- ✅ Full security header suite

## 📊 Changed Lines Summary

| File | Lines Changed | Type |
|------|---------------|------|
| main.tf | 57 | Added `filter {}` |
| main.tf | 97 | Added `filter {}` |
| main.tf | 183-235 | Restructured headers policy |
| TROUBLESHOOTING.md | New file | Added documentation |

## 💡 Notes

- These fixes are **backward compatible**
- No changes to Terraform state required
- Existing deployments can be updated with `terraform apply`
- All other configuration remains unchanged

## 🆘 If You Still Have Issues

1. Check TROUBLESHOOTING.md for common errors
2. Ensure you're using AWS Provider version ~> 5.0
3. Run `terraform init -upgrade` to update providers
4. Verify AWS credentials are configured

## 📞 Quick Reference

```bash
# Full deployment from scratch
terraform init
terraform validate
terraform plan
terraform apply

# Update existing deployment
terraform plan
terraform apply

# If things go wrong
terraform destroy  # Remove everything
terraform apply    # Redeploy
```

---

**Version:** 2.0 (Fixed)  
**Date:** January 2026  
**Compatibility:** Terraform >= 1.5.0, AWS Provider ~> 5.0

Your Terraform configuration is now error-free and ready to deploy! 🚀

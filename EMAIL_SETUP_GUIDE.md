# 📧 Email Setup Guide for saad.mahmood@saherflow.com

## Quick Setup Steps

### 1. Update Your Email Password
In your `.env` file, replace:
```
EMAIL_PASS=your-actual-outlook-password
```

With your actual Outlook password for `saad.mahmood@saherflow.com`

### 2. Email Configuration Explained
- **EMAIL_HOST:** `outlook.office365.com` - The Outlook server that sends emails
- **EMAIL_PORT:** `587` - The secure port for email sending
- **EMAIL_USER:** `saad.mahmood@saherflow.com` - Your email address (sender)
- **EMAIL_PASS:** Your actual password - Used to authenticate with Outlook server

### 3. What Happens When Users Register?
1. User submits registration with company email (aramco.com, adnoc.ae, etc.)
2. System validates the domain is approved
3. System creates user account (unverified)
4. System sends verification email FROM `saad.mahmood@saherflow.com` TO user's email
5. User clicks verification link in email
6. User account becomes verified and can access all features

### 4. Test Your Setup
1. Update `EMAIL_PASS` in `.env` file
2. Restart server: `npm run dev`
3. Use Postman to register with: `test@aramco.com`
4. Check if verification email arrives at the test email address

### 5. Approved Company Domains Only
✅ **Allowed:**
- `@aramco.com` (Saudi Aramco)
- `@adnoc.ae` (ADNOC)
- `@qtm.com.qa` (QTM)
- `@pdo.co.om` (PDO)
- `@dnv.com` (DNV)

❌ **Rejected:**
- `@gmail.com`
- `@outlook.com`
- `@yahoo.com`
- Any other domain

### 6. Ready to Test!
Once you update the password, use the complete Postman testing guide to test all endpoints.
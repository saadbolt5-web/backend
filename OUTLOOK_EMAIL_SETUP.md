# Outlook Email Setup Guide for Saher Flow Solutions

## Email Configuration for saad.mahmood@saherflow.com

Since your Saher Flow domain is backed by Outlook, here's the complete setup process:

## Step 1: SMTP Settings (Already Configured)

The following settings are already configured in your `.env` file:
- **SMTP Host:** `smtp.office365.com`
- **Port:** `587`
- **Security:** TLS/STARTTLS
- **Email:** `saad.mahmood@saherflow.com`

## Step 2: Get Your Email Password

### Option A: Regular Password (Simplest)
1. Use your regular Outlook login password
2. Update `.env` file:
   ```
   EMAIL_PASS=your-regular-outlook-password
   ```

### Option B: App Password (More Secure - Recommended)
1. **Sign in to Microsoft Account:**
   - Go to https://account.microsoft.com/security
   - Sign in with saad.mahmood@saherflow.com

2. **Enable Two-Factor Authentication (if not already enabled):**
   - Go to "Advanced security options"
   - Set up two-step verification

3. **Create App Password:**
   - In "Advanced security options"
   - Click "Create a new app password"
   - Name it "Saher Flow API"
   - Copy the generated password (16 characters)

4. **Update .env file:**
   ```
   EMAIL_PASS=your-16-character-app-password
   ```

## Step 3: Alternative SMTP Settings (If Office365 doesn't work)

If `smtp.office365.com` doesn't work, try these alternatives:

### For Custom Domain on Outlook:
```
EMAIL_HOST=smtp-mail.outlook.com
EMAIL_PORT=587
```

### For Exchange Server:
```
EMAIL_HOST=outlook.office365.com
EMAIL_PORT=587
```

## Step 4: Test Email Configuration

1. **Start the server:**
   ```bash
   npm run dev
   ```

2. **Register a test user via Postman:**
   ```
   POST http://localhost:5000/api/auth/register
   ```

3. **Check console logs for:**
   - "Email sent: [message-id]" (success)
   - Any SMTP error messages (failure)

## Step 5: Common Issues & Solutions

### Issue: "Invalid login" or "Authentication failed"
**Solution:** 
- Verify email and password are correct
- Try using app password instead of regular password
- Check if 2FA is required

### Issue: "Connection timeout"
**Solution:**
- Try alternative SMTP hosts listed above
- Check if your network blocks SMTP ports
- Verify firewall settings

### Issue: "Relay access denied"
**Solution:**
- Ensure you're using the correct SMTP server for your domain
- Contact your IT admin if using corporate email

## Step 6: Security Considerations

1. **Never commit .env file to version control**
2. **Use app passwords instead of regular passwords**
3. **Enable 2FA on your Microsoft account**
4. **Regularly rotate app passwords**

## Step 7: Testing Email Templates

The system sends two types of emails:

### Welcome/Verification Email:
- **Subject:** "Welcome to Saher Flow Solutions - Verify Your Email"
- **Contains:** Verification link with 24-hour expiry
- **Styling:** Professional with Saher Flow branding

### Password Reset Email:
- **Subject:** "Password Reset Request - Saher Flow Solutions"
- **Contains:** Reset link with 10-minute expiry
- **Security:** Clear instructions about ignoring if not requested

## Troubleshooting Commands

### Test SMTP Connection (Optional):
Create a simple test file to verify SMTP settings:

```javascript
// test-email.js
const nodemailer = require('nodemailer');
require('dotenv').config();

const testEmail = async () => {
  const transporter = nodemailer.createTransporter({
    host: process.env.EMAIL_HOST,
    port: process.env.EMAIL_PORT,
    secure: false,
    auth: {
      user: process.env.EMAIL_USER,
      pass: process.env.EMAIL_PASS
    }
  });

  try {
    await transporter.verify();
    console.log('✅ SMTP connection successful!');
  } catch (error) {
    console.error('❌ SMTP connection failed:', error.message);
  }
};

testEmail();
```

Run with: `node test-email.js`

## Ready to Test?

Once you've updated the `EMAIL_PASS` in your `.env` file:

1. Restart the server: `npm run dev`
2. Follow the Postman testing guide
3. Register a user and check your saad.mahmood@saherflow.com inbox
4. Complete the verification flow

The system is now configured for your Outlook-backed Saher Flow email!
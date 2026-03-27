## SMTP Relay — Multi-Enrollment

Send emails through the UnitySVC SMTP gateway using your own SMTP servers. Unlike the simple BYOK service, this allows **multiple enrollments** — each enrollment connects to a different SMTP server.

### Use Cases

- **Personal + Work**: one enrollment for Gmail, another for your company's SMTP
- **Transactional + Marketing**: separate enrollments for SES (transactional) and Mailgun (marketing)
- **Multi-tenant**: different SMTP servers for different clients or projects

### Setup

1. **Create customer secrets** for each SMTP server you want to use. Use a naming convention to keep them organized:

   ```
   # First SMTP server (e.g., Gmail)
   GMAIL_HOST = smtp.gmail.com
   GMAIL_PORT = 587
   GMAIL_USER = you@gmail.com
   GMAIL_PASS = your-app-password

   # Second SMTP server (e.g., SendGrid)
   SG_HOST = smtp.sendgrid.net
   SG_PORT = 587
   SG_USER = apikey
   SG_PASS = SG.xxxxx
   ```

2. **Enroll** in this service, providing the secret names as parameters:

   For the Gmail enrollment:
   - `SMTP_HOST_SECRET` = `GMAIL_HOST`
   - `SMTP_PORT_SECRET` = `GMAIL_PORT`
   - `SMTP_USERNAME_SECRET` = `GMAIL_USER`
   - `SMTP_PASSWORD_SECRET` = `GMAIL_PASS`

   For the SendGrid enrollment:
   - `SMTP_HOST_SECRET` = `SG_HOST`
   - `SMTP_PORT_SECRET` = `SG_PORT`
   - `SMTP_USERNAME_SECRET` = `SG_USER`
   - `SMTP_PASSWORD_SECRET` = `SG_PASS`

3. **Send email** through each enrollment's unique gateway endpoint using your svcpass API key

### How It Works

Each enrollment resolves `${ customer_secrets.{{ params.SMTP_HOST_SECRET }} }` to look up the secret name from your enrollment parameters, then retrieves the actual credential from your customer secrets. This indirection allows the same service template to support unlimited SMTP configurations.

# Deploying An Otter Wiki on Railway

This guide will help you deploy An Otter Wiki on Railway.

## Prerequisites

- A Railway account (sign up at [railway.app](https://railway.app))
- A GitHub account (if deploying from a repository)

## Quick Deploy

### Option 1: Deploy from GitHub

1. Fork or push this repository to GitHub
2. Go to [Railway Dashboard](https://railway.app/dashboard)
3. Click "New Project"
4. Select "Deploy from GitHub repo"
5. Choose your repository
6. Railway will automatically detect the Dockerfile and start building

### Option 2: Deploy from CLI

1. Install Railway CLI:
   ```bash
   npm i -g @railway/cli
   ```

2. Login to Railway:
   ```bash
   railway login
   ```

3. Initialize and deploy:
   ```bash
   railway init
   railway up
   ```

## Configuration

### Environment Variables

Railway will automatically set the `PORT` environment variable. The application will use this to configure nginx.

You can set additional environment variables in the Railway dashboard:

#### Required (auto-generated if not set):
- `OTTERWIKI_SETTINGS` - Path to settings file (default: `/app-data/settings.cfg`)
- `OTTERWIKI_REPOSITORY` - Path to git repository (default: `/app-data/repository`)

#### Optional:
- `SECRET_KEY` - Secret key for session signing (auto-generated if not set)
- `SITE_NAME` - Name of your wiki (default: "Otterwiki")
- `SQLALCHEMY_DATABASE_URI` - Database URI (default: SQLite at `/app-data/db.sqlite`)
- `READ_ACCESS` - Access level for reading (default: "ANONYMOUS")
- `WRITE_ACCESS` - Access level for writing (default: "REGISTERED")
- `ATTACHMENT_ACCESS` - Access level for attachments (default: "REGISTERED")
- `AUTO_APPROVAL` - Auto-approve new users (default: "True")
- `EMAIL_NEEDS_CONFIRMATION` - Require email confirmation (default: "True")

#### Email Configuration (optional):
- `MAIL_SERVER` - SMTP server
- `MAIL_PORT` - SMTP port
- `MAIL_USE_TLS` - Use TLS (true/false)
- `MAIL_USE_SSL` - Use SSL (true/false)
- `MAIL_USERNAME` - SMTP username
- `MAIL_PASSWORD` - SMTP password
- `MAIL_DEFAULT_SENDER` - Default sender email

### Persistent Storage

Railway provides persistent storage for the `/app-data` directory. This includes:
- Settings file (`settings.cfg`)
- SQLite database (`db.sqlite`)
- Git repository with all wiki content

**Important**: Make sure to set up a Railway volume for persistent storage:
1. Go to your project in Railway dashboard
2. Click "New" → "Volume"
3. Mount it to `/app-data` in your service settings

## First Run

1. After deployment, access your wiki using the Railway-provided URL
2. Register your first account - this account will automatically be an admin
3. Go to Settings to configure your wiki
4. Customize the settings to your liking

## Custom Domain

1. In Railway dashboard, go to your service
2. Click on "Settings" → "Domains"
3. Add your custom domain
4. Railway will provide DNS instructions

## Troubleshooting

### Health Check

The application includes a health check endpoint at `/-/healthz`. Railway will use this to monitor the service.

### Logs

View logs in Railway dashboard:
1. Go to your service
2. Click on "Deployments"
3. Click on the latest deployment
4. View logs in real-time

### Database Issues

If you encounter database issues:
- Check that the `/app-data` volume is properly mounted
- Ensure the volume has write permissions
- Check logs for specific error messages

### Port Configuration

The application automatically uses Railway's `PORT` environment variable. If you need to override it, set `LISTEN_PORT` in your environment variables.

## Support

For more information:
- [Otter Wiki Documentation](https://otterwiki.com)
- [Railway Documentation](https://docs.railway.app)


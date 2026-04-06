# DEPLOYMENT GUIDE

## 🚀 Deploying ADI's Online Studio

### Option 1: Render.com (Recommended for Backend)

#### Step 1: Prepare Backend

```bash
# Add start script in server/package.json
"scripts": {
  "start": "node index.js",
  "dev": "nodemon index.js"
}
```

#### Step 2: Create Render Account

1. Go to https://render.com
2. Sign up with GitHub
3. Click "New +" → "Web Service"
4. Connect your GitHub repository

#### Step 3: Configure Backend

Service Settings:
- **Name**: adis-studio-backend
- **Environment**: Node
- **Build Command**: `npm install`
- **Start Command**: `npm start`
- **Region**: Choose closest to you

#### Step 4: Add Environment Variables

In Render Dashboard:
```
PORT=5000
MONGODB_URI=your_atlas_connection_string
JWT_SECRET=your_production_secret_key
JWT_EXPIRE=7d
EMAIL_USER=your_email@gmail.com
EMAIL_PASSWORD=your_app_password
NODE_ENV=production
```

#### Step 5: Deploy

Click "Create Web Service" - Render will automatically deploy on every GitHub push

**Your backend URL**: `https://your-service-name.onrender.com`

---

### Option 2: Railway.app (Alternative Backend)

#### Step 1: Sign Up

Go to https://railway.app and sign up with GitHub

#### Step 2: Create Project

Click "New Project" → "Deploy from GitHub repo"

#### Step 3: Add Environment Variables

In Railway dashboard, go to Variables and add:
```
PORT=5000
MONGODB_URI=your_mongodb_string
JWT_SECRET=your_secret
JWT_EXPIRE=7d
EMAIL_USER=your_email
EMAIL_PASSWORD=your_password
NODE_ENV=production
```

#### Step 4: Deploy

Railway auto-deploys on GitHub push

---

### Option 3: Vercel (Best for Frontend)

#### Step 1: Prepare Frontend

Update API base URL in `client/src/api.js`:
```javascript
const API = axios.create({
  baseURL: 'https://your-backend-url.com/api',  // Change this
});
```

#### Step 2: Deploy to Vercel

```bash
# Install Vercel CLI
npm install -g vercel

# Deploy
cd client
vercel
```

Or use GitHub:
1. Push code to GitHub
2. Go to https://vercel.com
3. Sign in with GitHub
4. Click "Add New..." → "Project"
5. Select your repo
6. Click "Import"
7. Deploy!

---

### GitHub Pages (Free Frontend Hosting)

#### Step 1: Update package.json

In `client/package.json`, add:
```json
"homepage": "https://yourusername.github.io/adis-studio",
"scripts": {
  "predeploy": "npm run build",
  "deploy": "gh-pages -d build"
}
```

#### Step 2: Install gh-pages

```bash
cd client
npm install --save-dev gh-pages
```

#### Step 3: Update API URL

In `client/src/api.js`, change:
```javascript
baseURL: 'https://your-render-backend.onrender.com/api'
```

#### Step 4: Deploy

```bash
npm run deploy
```

Your site will be at: `https://yourusername.github.io/adis-studio`

---

## 📊 MongoDB Atlas Setup (Database)

#### Step 1: Create Account

1. Go to https://www.mongodb.com/cloud/atlas
2. Create free account
3. Create organization and project

#### Step 2: Create Cluster

1. Click "Create Deployment"
2. Choose "Free" tier
3. Select region (closer = faster)
4. Click "Create"

#### Step 3: Create Database User

1. Go to "Database Access"
2. Click "Add New Database User"
3. Create username and strong password
4. Click "Create User"

#### Step 4: Allow Network Access

1. Go to "Network Access"
2. Click "Add IP Address"
3. Choose "Allow Access from Anywhere" (0.0.0.0/0) for development
4. Restrict IPs in production

#### Step 5: Get Connection String

1. Go to "Databases"
2. Click "Connect" on your cluster
3. Choose "Connect your application"
4. Select "Node.js"
5. Copy connection string
6. Replace `<password>` with your database user password

Connection string format:
```
mongodb+srv://username:password@cluster0.mongodb.net/adis_studio?retryWrites=true&w=majority
```

#### Step 6: Add to Environment Variables

In your backend deployment platform:
```
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/adis_studio
```

---

## 🔒 Security Checklist

Before Production:

- [ ] Change JWT_SECRET to strong random string
- [ ] Change EMAIL_PASSWORD (use app password, not main password)
- [ ] Set NODE_ENV=production
- [ ] Update API base URL in frontend
- [ ] Restrict MongoDB network access to your server IP
- [ ] Enable HTTPS (automatic on Render/Vercel)
- [ ] Set up CORS properly for your domain
- [ ] Use environment variables for all secrets
- [ ] Test payment processing (if applicable)
- [ ] Set up error logging

---

## 📈 Environment-Specific Setup

### Development (.env)
```
PORT=5000
MONGODB_URI=mongodb://localhost:27017/adis_studio
JWT_SECRET=dev_secret_key
NODE_ENV=development
```

### Production (.env)
```
PORT=5000
MONGODB_URI=mongodb+srv://user:password@cluster.mongodb.net/adis_studio
JWT_SECRET=strong_random_production_secret
NODE_ENV=production
```

---

## 🔄 Update Workflow

### For Backend Updates

```bash
git add .
git commit -m "Update backend"
git push origin main
# Render/Railway auto-deploys!
```

### For Frontend Updates

```bash
cd client
git add .
git commit -m "Update frontend"
git push origin main
# Vercel/GitHub Pages auto-deploys!
```

---

## 📊 Monitor Deployment

### Render Dashboard
- View logs
- Check deployment status
- Monitor resource usage
- Check error logs

### Vercel Dashboard
- View deployment history
- Check analytics
- Review errors
- Monitor performance

### MongoDB Atlas
- Check cluster status
- Monitor metrics
- Review backups
- Check alerts

---

## 🆘 Troubleshooting Deployment

### Backend won't deploy
- Check syntax errors: `npm run dev` locally
- Verify .env variables are set
- Check GitHub repo is up to date
- Review deployment logs

### Frontend not connecting to backend
- Verify backend URL in `api.js`
- Check CORS settings in backend
- Ensure backend is running
- Test with curl: `curl https://your-backend/api/health`

### Database connection fails
- Verify MongoDB connection string
- Check IP whitelist in Atlas
- Test connection locally first
- Review network access settings

### Emails not sending
- Verify Gmail app password
- Check credentials in .env
- Test locally first
- Review Gmail security alerts

---

## 🎯 Post-Deployment Steps

1. **Test all features**
   - Register new user
   - Upload photo
   - Download photo
   - Check admin panel

2. **Set up email forwarding** (optional)
   - Redirect to your business email

3. **Configure domain** (if you have one)
   - Update DNS records
   - Set up SSL certificate
   - Update API URL

4. **Monitor performance**
   - Check response times
   - Monitor errors
   - Track user activity

5. **Set up backups**
   - MongoDB Atlas backups (automatic)
   - GitHub as code backup
   - Regular database exports

---

## 📞 Production Support

### Before Going Live

- [ ] Test all workflows
- [ ] Set up monitoring/alerts
- [ ] Create admin account
- [ ] Backup database
- [ ] Document deployment details
- [ ] Have rollback plan

### Ongoing

- [ ] Monitor logs daily
- [ ] Update dependencies monthly
- [ ] Backup database weekly
- [ ] Review analytics
- [ ] Update content regularly

---

## 🎉 You're Live!

Your premium studio application is now live and ready for customers!

Share your amazing work:
- 📱 Social media
- 📧 Email marketing
- 🔗 Direct link
- 💼 Business listing

---

**Need help? Check logs in your deployment dashboard!**

# QUICK START GUIDE

## Step 1: MongoDB Setup (2 minutes)

1. Go to https://www.mongodb.com/cloud/atlas
2. Create free account
3. Create new cluster (choose free tier)
4. Create database user with password
5. Add your IP to Network Access
6. Get connection string: `mongodb+srv://user:password@cluster.mongodb.net/adis_studio`

## Step 2: Gmail Setup (3 minutes)

1. Enable 2-Factor Authentication on Google Account
2. Go to https://myaccount.google.com/apppasswords
3. Generate app password for Mail
4. Copy the 16-character password

## Step 3: Backend Installation (5 minutes)

```bash
# Navigate to server folder
cd server

# Install dependencies
npm install

# Create .env file with:
PORT=5000
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=super_secret_key_change_this
JWT_EXPIRE=7d
EMAIL_USER=your_gmail@gmail.com
EMAIL_PASSWORD=your_16_char_app_password
NODE_ENV=development

# Start development server
npm run dev
```

Server will run on: **http://localhost:5000**

## Step 4: Frontend Installation (5 minutes)

```bash
# Navigate to client folder (in new terminal)
cd client

# Install dependencies
npm install

# Start development server
npm start
```

App will open on: **http://localhost:3000**

## Step 5: Test the App

### Test Account 1 (Regular User)
```
Email: user@example.com
Password: password123
```

First time: Click "Sign Up" and register with these credentials

### Test Account 2 (Admin User)
Create a regular account first, then:
1. In database, change user `role` to `"admin"`
2. Or contact the admin panel via database

### Test Flow:
1. ✅ Register
2. ✅ Login
3. ✅ Upload a photo
4. ✅ View dashboard gallery
5. ✅ Visit portfolio
6. ✅ Check pricing calculator
7. ✅ Admin: Visit admin panel (if admin user)

## 🔧 Useful Commands

### Backend
```bash
npm run dev      # Start with nodemon (auto-reload)
npm start        # Start production
```

### Frontend
```bash
npm start        # Start dev server
npm run build    # Build for production
npm test         # Run tests
```

## 🌐 Project Links

- Website: http://localhost:3000
- API: http://localhost:5000
- API Health: http://localhost:5000/api/health

## 📂 Important Files to Know

| File | Purpose |
|------|---------|
| `server/.env` | Backend configuration |
| `server/index.js` | Main server entry |
| `server/models/User.js` | User database schema |
| `server/models/Photo.js` | Photo database schema |
| `client/src/api.js` | Frontend API calls |
| `client/src/context/AuthContext.js` | Authentication logic |

## ⚠️ Common Issues

### "Cannot find module"
```bash
# Reinstall dependencies
npm install
```

### "ECONNREFUSED 127.0.0.1:5000"
Backend not running. Run `npm run dev` in server folder.

### "MongoDB connection failed"
Check MONGODB_URI in .env matches your cluster.

### "Email not sending"
Verify EMAIL_USER and EMAIL_PASSWORD in .env

### Port already in use
Change PORT in .env or kill existing process

## 📱 WhatsApp Integration

Edit the phone number in `client/src/components/WhatsAppButton.jsx`:
```javascript
const phoneNumber = '+1234567890'; // Add your phone number
```

## 🎨 Customize Branding

Edit in `client/src/components/Navbar.jsx`:
```javascript
<Link to="/" className="text-2xl font-bold text-white">
  YOUR STUDIO NAME
</Link>
```

## 🚀 Ready for Deployment!

### Deploy Backend (Render.com example)
1. Push code to GitHub
2. Create Render account
3. Connect GitHub repo
4. Add environment variables
5. Deploy!

### Deploy Frontend (GitHub Pages)
```bash
cd client
npm run build
# Upload 'build' folder to GitHub Pages
```

---

**That's it! Your premium studio app is ready! 🎉**

Need help? Check the full README.md in the root folder.

# ADI's Online Studio - Installation & Setup Instructions

## 📋 Prerequisites

Before starting, make sure you have:
- **Node.js** (v14 or higher) - Download from https://nodejs.org
- **npm** (comes with Node.js)
- **Git** (optional, for version control)
- **A Text Editor** (VS Code recommended)

## 🔧 Complete Installation Guide

### Phase 1: Database Setup (MongoDB Atlas)

**Time: 5-10 minutes**

1. **Create MongoDB Account**
   - Go to https://www.mongodb.com/cloud/atlas
   - Click "Try Free"
   - Sign up with email

2. **Create Organization**
   - Organization Name: "ADI Studio"
   - Click "Create Organization"

3. **Create Project**
   - Project Name: "ADI Online Studio"
   - Click "Create Project"

4. **Create Cluster**
   - Click "Create" → Select "Free" tier
   - Provider: AWS (recommended)
   - Region: Choose closest to you
   - Click "Create Cluster"
   - Wait 3-5 minutes for cluster to ready

5. **Create Database User**
   - Click "Database Access" (left sidebar)
   - Click "Add New Database User"
   - Username: `admin`
   - Password: Create strong password (save this!)
   - Built-in roles: `Atlas admin`
   - Click "Add User"

6. **Configure Network Access**
   - Click "Network Access" (left sidebar)
   - Click "Add IP Address"
   - Click "Allow Access from Anywhere"
   - Confirm

7. **Get Connection String**
   - Click "Databases" on the left
   - Click "Connect" on your cluster
   - Select "Connect your application"
   - Choose "Node.js" and version "4.x or later"
   - Copy the connection string
   - Replace `<password>` with your database password
   - Replace `admin` with `adis_studio` (database name)

   Example:
   ```
   mongodb+srv://admin:password123@cluster0.mongodb.net/adis_studio?retryWrites=true&w=majority
   ```

### Phase 2: Gmail Setup (Email Notifications)

**Time: 5 minutes**

1. **Enable 2-Factor Authentication**
   - Go to https://myaccount.google.com/security
   - Click "2-Step Verification"
   - Follow setup process

2. **Create App Password**
   - Go to https://myaccount.google.com/apppasswords
   - Select "Mail" and "Windows Computer" (or your OS)
   - Click "Generate"
   - Google will show you a 16-character password
   - **SAVE THIS PASSWORD** - You'll need it soon

### Phase 3: Backend Installation

**Time: 10-15 minutes**

1. **Navigate to Server Folder**
   ```bash
   cd server
   ```

2. **Install Dependencies**
   ```bash
   npm install
   ```
   This will install all required packages (may take 2-3 minutes)

3. **Create .env File**
   - In the `server` folder, create new file named `.env`
   - Add these values:

   ```
   PORT=5000
   MONGODB_URI=mongodb+srv://admin:your_password@cluster0.mongodb.net/adis_studio?retryWrites=true&w=majority
   JWT_SECRET=your_super_secret_jwt_key_change_this_in_production_12345
   JWT_EXPIRE=7d
   EMAIL_USER=your_gmail@gmail.com
   EMAIL_PASSWORD=your_16_char_app_password
   NODE_ENV=development
   ```

   **Replace with your actual values:**
   - `your_password` - MongoDB password you created
   - `your_gmail@gmail.com` - Your Gmail address
   - `your_16_char_app_password` - App password from Gmail setup

4. **Test Backend**
   ```bash
   npm run dev
   ```

   You should see:
   ```
   Server running on port 5000
   MongoDB Connected: cluster0.mongodb.net
   ```

   **Leave this running!** Open a new terminal for the frontend.

### Phase 4: Frontend Installation

**Time: 10-15 minutes**

1. **Navigate to Client Folder** (in a NEW terminal window)
   ```bash
   cd client
   ```

2. **Install Dependencies**
   ```bash
   npm install
   ```
   This installs React and all required packages

3. **Start Frontend Server**
   ```bash
   npm start
   ```

   The app will automatically open at `http://localhost:3000`

   You should see the ADI's Studio homepage with smooth animations!

## ✅ Verification Checklist

Make sure everything is working:

- [ ] Backend running (port 5000)
- [ ] Frontend running (port 3000)
- [ ] Can see the homepage with animations
- [ ] Can register a new account
- [ ] Can login with that account
- [ ] Email received after registration
- [ ] Can upload photos
- [ ] Photos appear in dashboard
- [ ] Can download photos

## 🧪 Testing the App

### Test Flow 1: User Registration & Upload
1. Go to http://localhost:3000
2. Click "Sign Up"
3. Fill in name, email, password
4. Check your email (should receive welcome email)
5. Go to Dashboard
6. Upload a photo
7. Photo should appear in gallery

### Test Flow 2: Portfolio Viewing
1. Click "Portfolio" in navigation
2. Should see all uploaded photos
3. Hover over photos to see preview

### Test Flow 3: Admin Functions
1. First, you need an admin account
2. After registering, go to MongoDB Atlas
3. Find your user in `adis_studio` → `users` collection
4. Change the `role` field from `"user"` to `"admin"`
5. Refresh the browser
6. You should now see "Admin" link in navigation
7. Go to Admin panel to manage users and photos

## 🆘 Troubleshooting

### "npm: command not found"
- **Solution**: Install Node.js from https://nodejs.org
- Restart terminal/computer after installation

### "Cannot find module 'express'"
```bash
# In the server folder, run:
npm install
```

### "ECONNREFUSED localhost:5000"
- **Check**: Is backend running? (`npm run dev` in server folder)
- Make sure you have TWO terminal windows open

### "ECONNREFUSED localhost:27017" (local MongoDB)
- **Solution**: You're not using MongoDB Atlas correctly
- Verify MONGODB_URI in .env starts with `mongodb+srv://`

### "MongoDB connection failed"
- ✓ Check MongoDB_URI in .env
- ✓ Check username/password spelling
- ✓ Check IP is whitelisted in MongoDB Atlas
- ✓ Verify database user was created

### "Email not sending"
- ✓ Check Gmail credentials in .env
- ✓ Verify it's the 16-char APP PASSWORD (not real password)
- ✓ Check 2-Factor Authentication is enabled
- ✓ Verify "Less secure app access" settings (if needed)

### "Port already in use"
Change port in `.env`:
```
PORT=5001  # Try different port
```

### Blank page or white screen
- Open browser console (F12)
- Check for error messages
- Usually means API calls are failing
- Verify backend is running

## 📚 File Locations You'll Need

| Task | File |
|------|------|
| Change database connection | `server/.env` |
| Change email settings | `server/.env` |
| Change API base URL | `client/src/api.js` |
| Change WhatsApp number | `client/src/components/WhatsAppButton.jsx` |
| Change studio name | `client/src/components/Navbar.jsx` |
| Change brand colors | `client/tailwind.config.js` |

## 🚀 Next Steps

After everything is working:

1. **Customize Content**
   - Update studio name
   - Add your photos
   - Change WhatsApp number
   - Update contact info

2. **Test All Features**
   - Registration/Login
   - Photo upload/download
   - Admin panel
   - Email receipts
   - Booking system

3. **Prepare for Deployment**
   - Read DEPLOYMENT.md
   - Set up production accounts
   - Test payment processing (if needed)
   - Get domain name (optional)

4. **Deploy to Production**
   - Backend to Render.com or Railway
   - Frontend to Vercel or GitHub Pages
   - Database already on MongoDB Atlas

## 📞 Quick Help Commands

```bash
# Start backend
cd server && npm run dev

# Start frontend  (new terminal)
cd client && npm start

# Install dependencies
npm install

# Check Node version
node --version

# Check npm version
npm --version
```

## ✨ You're All Set!

Your premium studio application is now running locally! 

Next step: **Read QUICKSTART.md** for testing the features.

Then: **Read DEPLOYMENT.md** for takes it to production.

---

**Questions? Check the error messages in the terminal or console (F12 in browser).**

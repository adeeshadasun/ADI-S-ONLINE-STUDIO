# ADI'S ONLINE STUDIO

Premium Digital Creative Studio Platform - Production Ready

## 🎨 Features

- **Premium Design**: Black & White luxury theme with glassmorphism
- **Authentication**: JWT-based secure authentication
- **Photo Management**: Upload, store, and manage photos
- **User Dashboard**: Personal gallery with download functionality
- **Admin Panel**: Complete control over users and content
- **Booking System**: Service booking and calendar
- **Loyalty Rewards**: Points and tier system
- **Email Receipts**: Automatic email confirmations
- **WhatsApp Integration**: Quick contact via WhatsApp
- **Pricing Calculator**: Dynamic service pricing
- **Modern Animations**: Smooth, cinematic UI transitions

## 🛠️ Tech Stack

### Backend
- Node.js + Express.js
- MongoDB + Mongoose
- JWT Authentication
- Nodemailer for emails
- Multer for file uploads

### Frontend
- React.js
- Tailwind CSS
- Framer Motion (animations)
- Axios for API calls
- React Router for navigation

## 📁 Project Structure

```
ADI'S ONLINE STUDIO/
├── server/              # Backend
│   ├── config/         # Database & email config
│   ├── models/         # MongoDB schemas
│   ├── controllers/    # Business logic
│   ├── routes/         # API endpoints
│   ├── middleware/     # Auth & upload
│   ├── uploads/        # Photo uploads
│   ├── package.json
│   ├── .env
│   └── index.js       # Main server file
│
├── client/             # Frontend
│   ├── public/        # Static files
│   ├── src/
│   │   ├── components/  # Reusable components
│   │   ├── pages/      # Route pages
│   │   ├── context/    # React context
│   │   ├── api.js      # API calls
│   │   ├── App.jsx
│   │   └── index.js
│   ├── package.json
│   ├── tailwind.config.js
│   └── postcss.config.js
│
└── README.md

```

## 🚀 Getting Started

### Prerequisites
- Node.js (v14+)
- MongoDB account (MongoDB Atlas)
- npm or yarn

### Installation

#### 1. Backend Setup

```bash
cd server
npm install
```

Configure `.env`:
```
PORT=5000
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/adis_studio
JWT_SECRET=your_secret_key_here
JWT_EXPIRE=7d
EMAIL_USER=your_email@gmail.com
EMAIL_PASSWORD=your_app_password
NODE_ENV=development
```

Run development server:
```bash
npm run dev
```

#### 2. Frontend Setup

```bash
cd client
npm install
npm start
```

The app will open at `http://localhost:3000`

## 🔐 Authentication

The app uses JWT (JSON Web Tokens) for secure authentication:
- Passwords hashed with bcrypt
- Tokens stored in localStorage
- Protected routes for authenticated users
- Admin-only routes for admin features

## 📝 API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `GET /api/auth/me` - Get current user

### Photos
- `POST /api/photos/upload` - Upload photo
- `GET /api/photos` - Get all photos
- `GET /api/photos/user/:userId` - Get user photos
- `GET /api/photos/:id` - Get single photo
- `GET /api/photos/:id/download` - Download photo
- `DELETE /api/photos/:id` - Delete photo

### Bookings
- `POST /api/bookings` - Create booking
- `GET /api/bookings/user/:userId` - Get user bookings
- `GET /api/bookings/:id` - Get booking
- `PUT /api/bookings/:id` - Update booking
- `DELETE /api/bookings/:id` - Cancel booking

### Admin (Admin only)
- `GET /api/admin/dashboard` - Dashboard stats
- `GET /api/admin/users` - All users
- `DELETE /api/admin/users/:id` - Delete user
- `PUT /api/admin/users/:id/role` - Change user role
- `POST /api/admin/photos/upload/:userId` - Upload for user
- `DELETE /api/admin/photos/:id` - Delete photo

## 🎯 User Features

### For Regular Users
1. Register & Login
2. Upload photos to personal gallery
3. View and download photos
4. Book services
5. View pricing
6. Contact via WhatsApp
7. Track loyalty points

### For Admin Users
1. View all users
2. Delete users
3. Upload photos to user galleries
4. Delete photos
5. View dashboard statistics
6. Manage bookings
7. Full system control

## 🎨 UI Components

- **Hero Section**: Animated title and CTA
- **Services Cards**: Glassmorphic cards with hover effects
- **Auth Forms**: Smooth, focused input styling
- **Dashboard**: User-friendly photo gallery
- **Admin Panel**: Clean data tables and management
- **Loading States**: Smooth spinner animations
- **Toast Notifications**: Non-intrusive feedback

## 📧 Email System

Automatic emails sent for:
- User registration (welcome)
- Photo uploads (receipt)
- Booking confirmations
- Service updates

Configure Gmail:
1. Enable 2FA on Gmail
2. Generate app password
3. Add to `.env` as `EMAIL_PASSWORD`

## 🌐 Deployment

### Frontend (GitHub Pages)

```bash
cd client
npm run build
# Deploy the build folder to GitHub Pages
```

### Backend (Render or Railway)

1. Push code to GitHub
2. Create account on Render.com or Railway.app
3. Connect GitHub repo
4. Set environment variables
5. Deploy

#### Environment Variables for Production:
```
MONGODB_URI=production_mongodb_uri
JWT_SECRET=strong_secret_key
EMAIL_USER=verified_email
EMAIL_PASSWORD=app_password
NODE_ENV=production
```

### Database (MongoDB Atlas)

1. Create cluster on MongoDB Atlas
2. Set up database user
3. Add IP whitelist
4. Get connection string
5. Add to MONGODB_URI in .env

## 🔒 Security Best Practices

✅ JWT token authentication
✅ Password hashing with bcrypt
✅ CORS enabled
✅ Input validation
✅ Protected routes
✅ File upload restrictions
✅ Role-based access control

## 📱 Responsive Design

- Mobile-first approach
- Tailwind CSS breakpoints
- Touch-friendly buttons
- Optimized images
- Fast loading

## 🚀 Performance

- Lazy loading images
- Code splitting
- Optimized animations
- Efficient database queries
- Caching strategies

## 🐛 Troubleshooting

### Backend won't connect to MongoDB
- Verify connection string
- Check IP whitelist on Atlas
- Ensure .env file is configured

### Frontend API calls failing
- Check CORS settings
- Verify backend is running on port 5000
- Check API base URL in api.js

### Email not sending
- Verify Gmail credentials
- Check app password (not regular password)
- Enable "Less secure app access" if needed

### File upload issues
- Check upload folder permissions
- Verify file size limits
- Ensure supported image formats

## 📞 Support

For issues or improvements:
1. Check error logs
2. Review API responses
3. Verify environment variables
4. Test with curl/Postman

## 📄 License

MIT License - Open for commercial use

## 🎯 Future Enhancements

- [ ] Video upload support
- [ ] Payment integration
- [ ] Advanced analytics
- [ ] Social sharing
- [ ] API rate limiting
- [ ] Image optimization
- [ ] Advanced filtering
- [ ] Real-time notifications

---

Built with ❤️ for premium creative services

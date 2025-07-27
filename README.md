# Bulk Buy Buddy 🌾

**Empowering Street Food Vendors with Smart Sourcing**

Bulk Buy Buddy is a comprehensive platform that connects street food vendors with suppliers, enabling bulk purchasing to reduce costs and streamline the procurement process. The platform facilitates group buying, allowing vendors to access wholesale prices and trusted suppliers while focusing on what they do best - cooking amazing food.

## 🚀 Features

### For Vendors
- **Supplier Discovery**: Search for suppliers by pincode to find local sources
- **Product Browsing**: View available products from suppliers with pricing and quantity information
- **Bulk Order Participation**: Join existing bulk orders to benefit from wholesale pricing
- **Order Management**: Track and manage individual orders
- **Location-based Search**: Find suppliers in your area using pincode filtering

### For Suppliers
- **Product Management**: Add, edit, and delete products with pricing and inventory details
- **Bulk Order Creation**: Create bulk orders with minimum quantity requirements (50kg+)
- **Dashboard Analytics**: Monitor product performance and order statistics
- **Order Tracking**: View and manage incoming orders from vendors
- **Business Profile**: Maintain business information and contact details

### General Features
- **Role-based Authentication**: Separate login systems for vendors and suppliers
- **Responsive Design**: Mobile-friendly interface built with Tailwind CSS
- **Real-time Updates**: Dynamic content updates without page refreshes
- **Secure Authentication**: JWT-based authentication with bcrypt password hashing

## 🛠️ Technology Stack

### Frontend
- **React 19.1.0**: Modern React with hooks and context API
- **React Router DOM 7.7.1**: Client-side routing and navigation
- **Tailwind CSS 3.4.17**: Utility-first CSS framework for responsive design
- **Axios 1.11.0**: HTTP client for API communication
- **CRACO**: Create React App Configuration Override for custom builds

### Backend
- **Node.js**: JavaScript runtime environment
- **Express.js 5.1.0**: Web application framework
- **MongoDB**: NoSQL database for data storage
- **Mongoose 8.16.5**: MongoDB object modeling for Node.js
- **JWT (jsonwebtoken 9.0.2)**: Token-based authentication
- **bcryptjs 3.0.2**: Password hashing and security
- **CORS 2.8.5**: Cross-origin resource sharing middleware
- **dotenv 17.2.1**: Environment variable management

## 📁 Project Structure

```
bulk-buy-buddy/
├── backend/
│   ├── models/
│   │   ├── User.js          # User schema (vendors & suppliers)
│   │   ├── Product.js       # Product schema
│   │   ├── Order.js         # Individual order schema
│   │   └── BulkOrder.js     # Bulk order schema
│   ├── routes/
│   │   ├── authRoutes.js    # Authentication endpoints
│   │   ├── vendor.js        # Vendor-specific routes
│   │   ├── supplier.js      # Supplier-specific routes
│   │   ├── products.js      # Product management routes
│   │   ├── orders.js        # Order management routes
│   │   └── bulkOrders.js    # Bulk order routes
│   ├── server.js            # Main server configuration
│   ├── package.json         # Backend dependencies
│   └── .env                 # Environment variables
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── AddProductModal.js      # Product creation modal
│   │   │   └── CreateBulkOrderModal.js # Bulk order creation modal
│   │   ├── context/
│   │   │   └── AuthContext.js          # Authentication context
│   │   ├── pages/
│   │   │   ├── HomePage.js             # Landing page
│   │   │   ├── LoginPage.js            # User authentication
│   │   │   ├── SignupPage.js           # User registration
│   │   │   ├── VendorDashboard.js      # Vendor main interface
│   │   │   ├── SupplierDashboard.js    # Supplier main interface
│   │   │   ├── SupplierProducts.js     # Product listing page
│   │   │   └── MyOrder.js              # Order management page
│   │   ├── App.js                      # Main application component
│   │   └── index.js                    # Application entry point
│   ├── public/                         # Static assets
│   ├── package.json                    # Frontend dependencies
│   ├── tailwind.config.js              # Tailwind CSS configuration
│   ├── craco.config.js                 # CRACO configuration
│   └── .env                            # Frontend environment variables
└── README.md
```

## 🗄️ Database Schema

### User Model
```javascript
{
  role: String,           // 'vendor' or 'supplier'
  name: String,           // User's name
  business_name: String,  // Business name (for suppliers)
  email: String,          // Email address
  phone: String,          // Phone number
  password: String,       // Hashed password
  pincode: String         // Location pincode
}
```

### Product Model
```javascript
{
  name: String,           // Product name
  quantity: Number,       // Available quantity in kg
  price: Number,          // Price per kg
  supplierId: ObjectId,   // Reference to supplier
  timestamps: true        // Created/updated timestamps
}
```

### Order Model
```javascript
{
  productId: ObjectId,    // Reference to product
  supplierId: ObjectId,   // Reference to supplier
  quantity: Number,       // Ordered quantity
  paymentMode: String,    // 'Cash on Delivery' or 'UPI Payment'
  createdAt: Date         // Order timestamp
}
```

### BulkOrder Model
```javascript
{
  productName: String,    // Product name
  quantity: Number,       // Minimum 50 kg
  price: Number,          // Price per kg
  supplierId: ObjectId,   // Reference to supplier
  supplierName: String,   // Supplier name
  pincode: String,        // Location pincode
  createdAt: Date         // Creation timestamp
}
```

## 🚀 Getting Started

### Prerequisites
- Node.js (v14 or higher)
- MongoDB (local installation or MongoDB Atlas)
- npm or yarn package manager

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd bulk-buy-buddy
   ```

2. **Backend Setup**
   ```bash
   cd backend
   npm install
   ```

3. **Frontend Setup**
   ```bash
   cd ../frontend
   npm install
   ```

4. **Environment Configuration**

   **Backend (.env)**
   ```env
   MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/bulk-buy-buddy
   PORT=5000
   JWT_SECRET=your-jwt-secret-key
   ```

   **Frontend (.env)**
   ```env
   REACT_APP_BACKEND_URL=http://localhost:5000
   REACT_APP_API_URL=http://localhost:5000
   ```

### Running the Application

1. **Start the Backend Server**
   ```bash
   cd backend
   npm start
   # Server will run on http://localhost:5000
   ```

2. **Start the Frontend Development Server**
   ```bash
   cd frontend
   npm start
   # Application will open at http://localhost:3000
   ```

## 🔐 Authentication Flow

### User Registration
- Users can register as either vendors or suppliers
- Vendors use phone numbers for authentication
- Suppliers can use either email or phone numbers
- Passwords are hashed using bcryptjs before storage

### Login Process
- Role-based login (vendor/supplier)
- JWT token generation for session management
- Token stored in localStorage for persistence
- Protected routes based on user roles

### Route Protection
- Public routes: Home, Login, Signup
- Vendor-only routes: Vendor Dashboard
- Supplier-only routes: Supplier Dashboard, Product Management
- Automatic redirection based on authentication status

## 🌐 API Endpoints

### Authentication
- `POST /api/auth/login` - User login
- `POST /api/auth/vendor` - Vendor registration
- `POST /api/auth/supplier` - Supplier registration

### Products
- `GET /api/products` - Get all products
- `POST /api/products` - Create new product
- `PUT /api/products/:id` - Update product
- `DELETE /api/products/:id` - Delete product

### Suppliers
- `GET /api/suppliers/search?pincode=` - Search suppliers by pincode

### Orders
- `GET /api/orders` - Get orders
- `POST /api/orders` - Create new order

### Bulk Orders
- `GET /api/bulk-orders` - Get all bulk orders
- `GET /api/bulk-orders/:supplierId` - Get supplier's bulk orders
- `POST /api/bulk-orders` - Create bulk order
- `PUT /api/bulk-orders/:id` - Update bulk order
- `DELETE /api/bulk-orders/:id` - Delete bulk order

## 🎨 UI/UX Features

### Design System
- **Color Palette**: Green primary (#059669), Orange secondary (#EA580C)
- **Typography**: Clean, readable fonts with proper hierarchy
- **Icons**: Emoji-based icons for visual appeal
- **Responsive**: Mobile-first design approach

### User Experience
- **Loading States**: Spinner animations during data fetching
- **Error Handling**: User-friendly error messages
- **Form Validation**: Client-side validation with helpful feedback
- **Modal Dialogs**: Smooth modal interactions for forms
- **Navigation**: Intuitive navigation with role-based menus

## 🔧 Development Tools

### Code Quality
- **ESLint**: JavaScript linting with React-specific rules
- **Prettier**: Code formatting (can be configured)
- **Git**: Version control with structured commits

### Build Tools
- **CRACO**: Custom React build configuration
- **PostCSS**: CSS processing with Tailwind
- **Autoprefixer**: Automatic CSS vendor prefixing

## 🚀 Deployment

### Frontend Deployment
The React application can be deployed to:
- Vercel
- Netlify
- AWS S3 + CloudFront
- GitHub Pages

Build command: `npm run build`

### Backend Deployment
The Node.js backend can be deployed to:
- Heroku
- AWS EC2
- DigitalOcean
- Railway

Ensure environment variables are properly configured in production.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the ISC License.

## 🆘 Support

For support and questions:
- Create an issue in the repository
- Contact the development team
- Check the documentation for common solutions

## 🔮 Future Enhancements

- **Payment Integration**: UPI and other payment gateways
- **Real-time Chat**: Communication between vendors and suppliers
- **Analytics Dashboard**: Advanced reporting and insights
- **Mobile App**: React Native mobile application
- **Notification System**: Email and SMS notifications
- **Rating System**: Vendor and supplier rating mechanism
- **Inventory Management**: Advanced stock tracking
- **Multi-language Support**: Localization for different regions

---

**Built with ❤️ for the street food vendor community**

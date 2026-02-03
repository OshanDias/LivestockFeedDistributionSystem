# 🐄 Livestock Feed Distribution System

A comprehensive Java Swing desktop application for managing livestock feed suppliers, products, farmers, and orders with inventory tracking and sales analytics.

![Java](https://img.shields.io/badge/Java-17-orange?style=flat&logo=java)
![MySQL](https://img.shields.io/badge/MySQL-8.0-blue?style=flat&logo=mysql)
![Swing](https://img.shields.io/badge/Swing-GUI-green?style=flat)
![JasperReports](https://img.shields.io/badge/JasperReports-6.20.0-red?style=flat)

## 📋 Table of Contents
- [Features](#features)
- [Screenshots](#screenshots)
- [Technology Stack](#technology-stack)
- [Database Schema](#database-schema)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Design Patterns](#design-patterns)
- [License](#license)

## ✨ Features

### 🔐 Authentication System
- Secure login with default credentials
- Session management

### 📦 Feed Supplier Management
- Add, update, delete, and search suppliers
- Track supplier ratings (0.0 - 5.0)
- Store contact information and business details
- Email and phone validation

### 🌱 Feed Product Management
- Manage multiple feed types (Grain, Pellets, Supplement, Mineral, Mixed)
- Livestock-specific products (Cattle, Poultry, Goat, Sheep, Pig)
- Real-time stock tracking
- Automatic stock reduction on orders
- Low stock alerts with reorder levels

### 👨‍🌾 Livestock Farmer Management
- Comprehensive farmer database
- Farm size and livestock count tracking
- NIC validation (Sri Lankan format)
- Search and filter functionality

### 🛒 Order Management (Main Transaction)
- Complete order processing workflow
- Automatic price calculation
- Stock reduction on order creation
- Payment status tracking (PENDING, PAID, PARTIAL)
- Delivery status tracking (PROCESSING, SHIPPED, DELIVERED, CANCELLED)
- Order filtering by status

### 📊 Sales Analytics & Reports
- Sales Analysis by Feed Type (3-table JOIN)
- Revenue analysis with grand totals
- Order statistics dashboard
- JasperReports integration

## 🖼️ Screenshots

### Dashboard - Sidebar Layout
```
┌─────────────────────────────────────────────┐
│  🐄 LIVESTOCK FEED DISTRIBUTION - DASHBOARD │
│                                             │
│  ┌──────┐  ┌──────────────────────────┐   │
│  │      │  │  Welcome Panel            │   │
│  │ Side │  │  Statistics Cards         │   │
│  │ bar  │  │  Quick Access            │   │
│  │      │  │                          │   │
│  │ Menu │  │  System Overview         │   │
│  └──────┘  └──────────────────────────┘   │
└─────────────────────────────────────────────┘
```

### CRUD Forms - Top-Bottom Layout
```
┌─────────────────────────────────────────────┐
│  ← BACK         SUPPLIER MANAGEMENT         │
├─────────────────────────────────────────────┤
│  ┌─────────────────────────────────────┐   │
│  │  INPUT FORM (2-Column Grid)         │   │
│  │  [Fields] [Fields]                  │   │
│  │  ➕ ADD  ✏️ UPDATE  🗑️ DELETE  🔄 CLEAR │
│  └─────────────────────────────────────┘   │
│  ┌─────────────────────────────────────┐   │
│  │  🔍 Search: [___________] SEARCH    │   │
│  │  ┌───────────────────────────────┐  │   │
│  │  │  Data Table (Full Width)      │  │   │
│  │  └───────────────────────────────┘  │   │
│  └─────────────────────────────────────┘   │
└─────────────────────────────────────────────┘
```

## 🛠️ Technology Stack

### Backend
- **Language:** Java 17
- **Database:** MySQL 8.0
- **JDBC:** MySQL Connector/J 9.6.0

### Frontend
- **GUI Framework:** Java Swing
- **Look and Feel:** System Native

### Reporting
- **JasperReports:** 6.20.0
- **iText:** 2.1.7

### Libraries
- Apache Commons Collections 4.4
- Apache Commons Logging 1.2
- Apache Commons BeanUtils 1.9.4
- Apache Commons Digester 2.1

## 🗄️ Database Schema

### Tables
1. **feed_suppliers** (8 fields)
   - Supplier information and ratings
   - Business registration details

2. **feed_products** (11 fields)
   - Product catalog with stock tracking
   - Feed type and livestock type classification
   - FK: supplier_id → feed_suppliers

3. **livestock_farmers** (11 fields)
   - Farmer registration and details
   - Farm size and livestock information

4. **feed_orders** (13 fields) - **Main Transaction Table**
   - Order processing and tracking
   - FK: farmer_id → livestock_farmers
   - FK: product_id → feed_products

### Relationships
```
feed_suppliers (1) ──→ (N) feed_products
livestock_farmers (1) ──→ (N) feed_orders
feed_products (1) ──→ (N) feed_orders
```

## 📥 Installation

### Prerequisites
- Java Development Kit (JDK) 17 or higher
- MySQL Server 8.0 or higher
- NetBeans IDE (recommended) or any Java IDE

### Steps

1. **Clone the repository**
```bash
   git clone https://github.com/yourusername/livestock-feed-distribution.git
   cd livestock-feed-distribution
```

2. **Set up the database**
```sql
   -- Run the SQL script in MySQL Workbench
   source database/livestock_feed_distribution.sql
```

3. **Configure database connection**
```java
   // Edit: src/com/feedsystem/dao/DatabaseConnection.java
   private static final String USERNAME = "your_mysql_username";
   private static final String PASSWORD = "your_mysql_password";
```

4. **Add required libraries**
   - Place JAR files in the `lib/` folder
   - Add to project build path:
     - mysql-connector-j-9.6.0.jar
     - jasperreports-6.20.0.jar
     - commons-collections4-4.4.jar
     - commons-logging-1.2.jar
     - commons-beanutils-1.9.4.jar
     - commons-digester-2.1.jar
     - itext-2.1.7.jar

5. **Build and run**
```bash
   # Using NetBeans: Clean and Build (Shift+F11)
   # Run: F6
   
   # Or using command line:
   javac -cp "lib/*" src/com/feedsystem/Main.java
   java -cp "lib/*:src" com.feedsystem.Main
```

## 🚀 Usage

### Login
- **Username:** `admin`
- **Password:** `admin123`

### Main Workflow

1. **Add Suppliers**
   - Navigate to Suppliers section
   - Fill in company details
   - Set supplier rating

2. **Manage Products**
   - Add feed products
   - Link to suppliers
   - Set stock levels and reorder points

3. **Register Farmers**
   - Enter farmer details
   - Specify livestock type and count
   - Validate NIC

4. **Process Orders**
   - Select farmer and product
   - Enter quantity
   - System calculates total
   - Stock automatically reduced
   - Track payment and delivery status

5. **Generate Reports**
   - View sales analysis by feed type
   - Export to PDF

## 📁 Project Structure
```
LivestockFeedDistributionSystem/
│
├── src/
│   └── com/
│       └── feedsystem/
│           ├── Main.java
│           ├── model/
│           │   ├── FeedSupplier.java
│           │   ├── FeedProduct.java
│           │   ├── LivestockFarmer.java
│           │   └── FeedOrder.java
│           ├── dao/
│           │   ├── DatabaseConnection.java
│           │   ├── FeedSupplierDAO.java
│           │   ├── FeedProductDAO.java
│           │   ├── LivestockFarmerDAO.java
│           │   └── FeedOrderDAO.java
│           ├── controller/
│           │   └── ReportController.java
│           ├── view/
│           │   ├── LoginForm.java
│           │   ├── DashboardForm.java
│           │   ├── SupplierForm.java
│           │   ├── ProductForm.java
│           │   ├── FarmerForm.java
│           │   └── OrderForm.java
│           └── util/
│               └── Validator.java
│
├── lib/
│   ├── mysql-connector-j-9.6.0.jar
│   ├── jasperreports-6.20.0.jar
│   └── [other libraries]
│
├── database/
│   └── livestock_feed_distribution.sql
│
├── dist/
│   └── LivestockFeedDistributionSystem.jar
│
└── README.md
```

## 🎨 Design Patterns

### 1. Singleton Pattern
- **DatabaseConnection:** Ensures single database connection instance

### 2. DAO Pattern
- Separate DAO for each entity
- Encapsulates database operations
- Clean separation of concerns

### 3. MVC Architecture
- **Model:** POJO classes (FeedSupplier, FeedProduct, etc.)
- **View:** Swing UI Forms
- **Controller:** ReportController, business logic

### 4. Utility Pattern
- **Validator:** Centralized input validation
- Reusable validation methods

## 🎨 UI Theme

**Purple/Magenta Professional Theme**
- Primary: RGB(142, 68, 173)
- Secondary: RGB(155, 89, 182)
- Accent: RGB(103, 58, 183)
- Success: RGB(46, 204, 113)
- Danger: RGB(231, 76, 60)

**Layout Style**
- Dashboard: Sidebar navigation (200px) + Main content area
- CRUD Forms: Top-Bottom layout with 2-column input grid
- Form Size: 1400x850

## 🔐 Security Features

- Password-protected login
- Input validation on all forms
- SQL injection prevention (PreparedStatements)
- NIC format validation (Sri Lankan)
- Email and phone number validation

## 📝 Validation Rules

- **Email:** Standard email format
- **Phone:** Sri Lankan format (0xxxxxxxxx)
- **NIC:** Old (9V/X) or New (12 digits) format
- **Rating:** 0.0 to 5.0
- **Stock:** Non-negative integers
- **Prices:** Positive decimals

## 🐛 Known Issues

- None reported

## 🔮 Future Enhancements

- [ ] User role management (Admin, Staff, Viewer)
- [ ] Advanced analytics dashboard
- [ ] Email notifications for low stock
- [ ] Backup and restore functionality
- [ ] Multi-language support
- [ ] Export to Excel
- [ ] Mobile app integration

## 👥 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.



## 🙏 Acknowledgments

- National Institute of Business Management (NIBM) 
- Java Swing Documentation
- JasperReports Community
- MySQL Documentation

## 📞 Support

For support, email Kawshika4114@gmail.com or open an issue in the GitHub repository.

---

⭐ **Star this repository if you find it helpful!**

**Built with ❤️ for livestock farmers and agricultural suppliers**

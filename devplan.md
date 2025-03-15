### **Gift Right Development Plan**

## **📌 Phase 1: Project Setup & Environment Configuration**
### **1.1 Repository & Development Environment**
✅ Set up a **GitHub repository** (`gift-right`)  
✅ Initialize the **directory structure** (Use the `setup.sh` script)  
✅ Create `.gitignore` and commit the base files  
✅ Install required dependencies:
   - PHP (with necessary extensions)
   - MariaDB/MySQL
   - Apache/Nginx (or PHP’s built-in server for development)

### **1.2 Database Configuration**
✅ Set up `config/database.php` for database connection  
✅ Create an `.env` file for storing credentials securely  
✅ Set up `database.php` with a PDO connection  

---

## **📌 Phase 2: User Authentication & Database Schema**
### **2.1 Database Schema (MariaDB/MySQL)**
#### **Tables to create first:**
- **users**
  - `id` (INT, Primary Key, Auto-increment)
  - `email` (VARCHAR, Unique)
  - `password` (VARCHAR, Hashed)
  - `name` (VARCHAR)
  - `province` (VARCHAR) *(for filtering gift requests)*
  - `created_at` (TIMESTAMP)
  - `updated_at` (TIMESTAMP)

- **sessions** *(for tracking logged-in users)*
  - `id` (INT, Primary Key, Auto-increment)
  - `user_id` (INT, Foreign Key)
  - `token` (VARCHAR, Unique)
  - `expires_at` (TIMESTAMP)

- **gifts**
  - `id` (INT, Primary Key, Auto-increment)
  - `user_id` (INT, Foreign Key)
  - `gift_name` (VARCHAR)
  - `category` (ENUM - Food, Hygiene, Medicine, Clothing, etc.)
  - `description` (TEXT)
  - `province` (VARCHAR)
  - `created_at` (TIMESTAMP)

- **admins**
  - `id` (INT, Primary Key, Auto-increment)
  - `email` (VARCHAR, Unique)
  - `password` (VARCHAR, Hashed)
  - `role` (ENUM - "superadmin", "moderator")
  - `created_at` (TIMESTAMP)

---

### **2.2 Implement User Authentication**
✅ **Create User Registration & Login system**
   - Use **password_hash()** for secure storage  
   - Validate input data (email format, password strength)  
   - Store session tokens in `sessions` table  

✅ **Session Management**
   - Implement `AuthController.php` for handling user authentication  
   - Store login sessions in `sessions` table  

✅ **Admin Authentication**
   - Create `admin-login.php` for admin access  
   - Only allow access to the admin panel if logged in  

---

## **📌 Phase 3: Gift Input System**
### **3.1 Gift Preferences Submission**
✅ **GiftController.php**
   - Handles adding, updating, and deleting gift preferences  
   - Ensures that users can only edit their own gifts  
   - Prevents duplicate submissions  

✅ **Gift Input Page**
   - Users can submit preferred gift types  
   - Categories are pre-defined (dropdown list)  
   - Store the province for localized recommendations  

---

## **📌 Phase 4: Reports & Traveler View**
### **4.1 Reports Page (`reports.php`)**
✅ **ReportController.php**
   - Queries `gifts` table based on the selected province  
   - Aggregates top requested gift types  

✅ **Metabase Integration**
   - If using Metabase, embed a simple reporting dashboard  

✅ **Frontend Filters**
   - Allow filtering by province and gift type  
   - Display results in a user-friendly format  

---

## **📌 Phase 5: Enhancements & Anti-Spam Measures**
### **5.1 Prevent Spam & Fake Accounts**
✅ **Email Verification**  
   - Send a confirmation email upon registration  

✅ **ReCAPTCHA/hCaptcha**  
   - Add to login and gift input pages  

✅ **Rate-Limiting & IP Tracking**  
   - Prevent rapid account creation  

✅ **Browser Language Detection**
   - Implement auto-detection for Spanish/English  

---

### **📌 Final Steps & Deployment**
- ✅ **Test all functionality** (Manual & Automated Testing)  
- ✅ **Deploy to a Live Server**  
- ✅ **Monitor performance & improve based on feedback**  

---

### **🌟 Summary of Priorities**
📍 **First to Build**:  
✅ Database schema & connection  
✅ User authentication (registration, login, session handling)  
✅ Admin authentication  

📍 **Next Steps**:  
✅ Gift input system  
✅ Reports page for travelers  

📍 **Future Enhancements**:  
🔜 Anti-spam protection  
🔜 Real-time updates (if needed)  
🔜 Advanced filtering  
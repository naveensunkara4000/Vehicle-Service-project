**Name:** Naveen Sunkara    
- **Duration:** December to April 2025  
---

# Instant Vehicle Service & Mechanic Locator (IVSML)

A web app that helps stranded drivers quickly **find nearby mechanics and spare-parts providers**, contact them, and track request status — minimizing downtime and stress during breakdowns.

> **Goal:** Fast, reliable, and user-friendly roadside assistance using location-based search and simple workflows.

---

## Overview of the Project

- Users can register/login, share their location (manual input), and **request a mechanic/service**.
- Admin manages users, mechanics, categories, and services.
- Mechanics can view **pending requests** and accept jobs.
- Built with a lightweight stack for easy local hosting and deployment.

---

## Objective

Reduce the time and effort to get help during unexpected breakdowns by providing a **centralized, location-based** platform that connects users to nearby, verified service providers.

---

## Tech Stack

- **Frontend:** HTML, CSS, JavaScript  
- **Backend:** PHP (procedural)  
- **Database:** MySQL  
- **Server (Local):** XAMPP/WAMP (Apache + MySQL + PHP)  
- **Optional Tools:** VS Code / PhpStorm, Postman (for manual request tests)

---

## Key Features

- ✨ **User Accounts:** Register/Login for users, mechanics, and admin roles  
- 📍 **Location-based Search:** Users submit current location to find nearby services  
- 🛠️ **Service Request Workflow:** Create, assign, accept, and complete requests  
- 🧰 **Mechanic Management:** Admin can add/view mechanics and services  
- 🗂️ **Categories & Services:** Define service categories (towing, repair, etc.)  
- 🔐 **Session & Basic Security:** Password hashing and session-based access

---

## Quick Start (Local Setup)

### 1) Prerequisites
- Install **XAMPP** or **WAMP** (Apache, PHP ≥ 7.4, MySQL ≥ 5.7)
- Create a MySQL user with access to a database named `vehicle_service` (or change the name in config)

### 2) Database Setup
1. Start **Apache** and **MySQL** from XAMPP/WAMP.
2. Open **phpMyAdmin** → Create database: `vehicle_service`.
3. Create the following minimal tables (you can expand as needed):

```sql
-- USERS (roles: user / mechanic / admin)
CREATE TABLE users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(150) NOT NULL UNIQUE,
  password VARCHAR(255) NOT NULL,
  role ENUM('user','mechanic','provider','admin') DEFAULT 'user',
  location VARCHAR(255),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- SERVICE REQUESTS
CREATE TABLE service_requests (
  id INT AUTO_INCREMENT PRIMARY KEY,
  user_id INT NOT NULL,
  mechanic_id INT NULL,
  location VARCHAR(255) NOT NULL,
  service_type VARCHAR(100) NOT NULL,
  status ENUM('pending','accepted','in_progress','completed','cancelled') DEFAULT 'pending',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);
```

> Note: Add more tables (e.g., `services`, `categories`) as your build requires.

### 3) Project Files & Config
- Place the project folder in your web root:
  - **XAMPP:** `C:\xampp\htdocs\ivsml`
  - **WAMP:** `C:\wamp64\www\ivsml`
- Create `includes/db.php` with your DB credentials:

```php
<?php
$conn = new mysqli("localhost", "root", "", "vehicle_service");
if ($conn->connect_error) {
  die("Connection failed: " . $conn->connect_error);
}
?>
```

### 4) Run the App
- Visit: `http://localhost/ivsml`
- Create an **admin** user directly in DB (or pre-seed), then login at `/admin/login.php` (path may vary based on your structure).

---

## Project Structure (Suggested)

```
ivsml/
├─ index.php                 # Landing/Home
├─ includes/
│  └─ db.php                 # Database connection
├─ user/
│  ├─ register.php           # User signup
│  ├─ login.php              # User login
│  └─ request_service.php    # Create a service request
├─ mechanic/
│  ├─ login.php
│  └─ dashboard.php          # View & accept pending requests
├─ admin/
│  ├─ login.php
│  ├─ dashboard.php          # KPIs/Counters
│  ├─ mechanics.php          # Manage mechanics
│  ├─ services.php           # Manage services
│  ├─ categories.php         # Manage categories
│  └─ users.php              # View users
└─ assets/
   ├─ css/
   ├─ js/
   └─ images/
```

> Adjust filenames/paths to match your implementation.

---

## How the Project Works (Step‑by‑Step with Screenshots)

### A) System Flow

1. **Start XAMPP Server**  
   _Launch XAMPP and start both Apache and MySQL services to run the application locally._  
   ![XAMPP Server Start](https://github.com/naveensunkara4000/Vehicle-Service-project/blob/8b41b0bbe5e5d04428a7dd0db55991342e79115b/Readme.md/Screenshorts/C1.png)

2. **Home Page Open**  
   _Open the application URL in your browser to view the home page interface._  
   ![Home Page](https://github.com/naveensunkara4000/Vehicle-Service-project/blob/8b41b0bbe5e5d04428a7dd0db55991342e79115b/Readme.md/Screenshorts/C2.png)

3. **Services We Offer**  
   _View a list of all available vehicle services (e.g., towing, repairs, battery replacement)._  
   ![Services](https://github.com/naveensunkara4000/Vehicle-Service-project/blob/8b41b0bbe5e5d04428a7dd0db55991342e79115b/Readme.md/Screenshorts/C3.png)

4. **Service Appointment Booking**  
   _Fill in the booking form by selecting service type, providing location, and preferred time._  
   ![Service Booking](https://github.com/naveensunkara4000/Vehicle-Service-project/blob/8b41b0bbe5e5d04428a7dd0db55991342e79115b/Readme.md/Screenshorts/C4.png)

5. **Booking Confirmation**  
   _Receive a confirmation message along with booking ID and service details._  
   ![Booking Confirmation](https://github.com/naveensunkara4000/Vehicle-Service-project/blob/8b41b0bbe5e5d04428a7dd0db55991342e79115b/Readme.md/Screenshorts/C5.png)

6. **Admin Login**  
   _Admin logs into the system to manage services, mechanics, and user requests._  
   ![Admin Login](https://github.com/naveensunkara4000/Vehicle-Service-project/blob/8b41b0bbe5e5d04428a7dd0db55991342e79115b/Readme.md/Screenshorts/C6.png)

7. **Dashboard**  
   _Admin dashboard showing key statistics like total users, bookings, and services._  
   ![Dashboard](https://github.com/naveensunkara4000/Vehicle-Service-project/blob/8b41b0bbe5e5d04428a7dd0db55991342e79115b/Readme.md/Screenshorts/C7.png)

8. **Mechanic List**  
   _View and manage the list of registered mechanics, their details, and availability._  
   ![Mechanic List](https://github.com/naveensunkara4000/Vehicle-Service-project/blob/8b41b0bbe5e5d04428a7dd0db55991342e79115b/Readme.md/Screenshorts/C8.png)

9. **Service Request List**  
   _Monitor all service requests made by users, including pending and completed ones._  
   ![Service Request List](https://github.com/naveensunkara4000/Vehicle-Service-project/blob/8b41b0bbe5e5d04428a7dd0db55991342e79115b/Readme.md/Screenshorts/C9.png)

10. **Reports**  
    _Generate and view reports summarizing bookings, services, and mechanic performance._  
    ![Reports](https://github.com/naveensunkara4000/Vehicle-Service-project/blob/8b41b0bbe5e5d04428a7dd0db55991342e79115b/Readme.md/Screenshorts/C10.png)

11. **Category List**  
    _Manage categories for different service types to organize offerings._  
    ![Category List](https://github.com/naveensunkara4000/Vehicle-Service-project/blob/8b41b0bbe5e5d04428a7dd0db55991342e79115b/Readme.md/Screenshorts/C11.png)

12. **Service List**  
    _View and edit the list of available services offered in each category._  
    ![Service List](https://github.com/naveensunkara4000/Vehicle-Service-project/blob/8b41b0bbe5e5d04428a7dd0db55991342e79115b/Readme.md/Screenshorts/C12.png)

13. **User List**  
    _Display all registered users with their contact details and booking history._  
    ![User List](https://github.com/naveensunkara4000/Vehicle-Service-project/blob/8b41b0bbe5e5d04428a7dd0db55991342e79115b/Readme.md/Screenshorts/C13.png)




---

## Core Pages & Paths (Typical)

- `/index.php` → Home/Landing  
- `/user/register.php` → Sign Up  
- `/user/login.php` → Login  
- `/user/request_service.php` → Create service request  
- `/mechanic/login.php` → Mechanic login  
- `/mechanic/dashboard.php` → Accept/track requests  
- `/admin/login.php` → Admin login  
- `/admin/dashboard.php` → KPIs & quick actions  
- `/admin/mechanics.php`, `/admin/services.php`, `/admin/categories.php`, `/admin/users.php`

---

## Security Notes

- Always **hash passwords** (e.g., `password_hash()` in PHP).
- Validate and sanitize **all inputs** (server‑side).
- Use **prepared statements** for DB queries.
- Restrict pages by **role-based checks** and sessions.

---

## Future Enhancements (Nice to Have)

- Real-time GPS & map integration  
- OTP/2FA for logins  
- Online payments (UPI/cards/wallets)  
- Rich review & rating system  
- Mobile app (Android/iOS) with push notifications

---

## Credits

Built by **Naveen Sunkara** as part of an academic project.  
Mentorship & guidance acknowledged.

---



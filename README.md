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

### A) User Flow
1. **Home → Explore Services**  
   _User lands on the home page and sees available service types._  
   `Readme.md/docs/screenshots/c2.png`

2. **Register / Login**  
   _Create an account or log in to continue._  
   `![Login](docs/screenshots/2-login.png)`

3. **Request Service**  
   _Open **Request Service** → enter current **Location** and select **Service Type** (e.g., Towing/Repair) → Submit._  
   `![Request Service](docs/screenshots/3-request-service.png)`

4. **Confirmation**  
   _You’ll see a confirmation (Request ID) and a **Pending** status while mechanics are notified._  
   `![Request Submitted](docs/screenshots/4-confirmation.png)`

5. **Status Updates**  
   _Once a mechanic accepts, status becomes **Accepted/In Progress** → After completion, it becomes **Completed**._  
   `![Request Status](docs/screenshots/5-status.png)`

### B) Mechanic Flow
6. **Mechanic Login**  
   _Mechanic logs in to see **Pending Requests** in dashboard._  
   `![Mechanic Login](docs/screenshots/6-mechanic-login.png)`

7. **Accept Request**  
   _Click **Accept** to take a job → request is assigned to this mechanic._  
   `![Mechanic Dashboard](docs/screenshots/7-mechanic-dashboard.png)`

### C) Admin Flow
8. **Admin Login**  
   _Admin logs in to manage the system._  
   `![Admin Login](docs/screenshots/8-admin-login.png)`

9. **Dashboard Overview**  
   _View counters: total users, mechanics, requests, etc._  
   `![Admin Dashboard](docs/screenshots/9-admin-dashboard.png)`

10. **Manage Mechanics / Services / Categories**  
    _Add/edit mechanics, define services & categories, review users._  
    `![Mechanics](docs/screenshots/10-mechanics.png)`  
    `![Services](docs/screenshots/11-services.png)`  
    `![Categories](docs/screenshots/12-categories.png)`  
    `![Users](docs/screenshots/13-users.png)`

> 📸 **Replacing the screenshots:** Put your PNG/JPG files under `docs/screenshots/` in your repo and keep the same filenames, or update the image paths here.  
> Tip: On GitHub, you can drag & drop images into an issue to get a public URL, then paste that URL in place of the relative paths above.

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

## License

Add a license file (e.g., MIT) if you plan to open-source the project.

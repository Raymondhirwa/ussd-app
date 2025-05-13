# 📱🎓 Marks Appeal System

A **Flask-based USSD and Web Admin Portal** that enables students to view and appeal academic marks via USSD, and allows administrators to manage these appeals through a secure web portal.
### GROUP MEMBERS:
```
21RP05800
22RP00164
22RP00282
22RP00535
22RP00789
22RP00751
22RP01008
22RP01016
22RP00730
22RP01442
```
### USAGE:
```
Dial *384*16673#
```
#### Admin : are using this link to aprove and track Marks Appeal (http://192.168.43.124:5000/admin/login)

**username:** ```hirwa```
**password:** ```12```

#### student table : use one student student_id as for Authantication
![image](https://github.com/user-attachments/assets/adbcd072-8f58-4cb0-a006-946db3762896)
#### Admin Table
![image](https://github.com/user-attachments/assets/c8c751d5-44dc-4a9d-8a0c-b491d857967f)

---

## 🚀 Features

### ✅ USSD Functionality (Student)
- View marks using Student ID
- Appeal specific module marks
- Check appeal status
- Automatic session timeout handling
- Input validation for smooth experience

### ✅ Admin Web Portal
- Admin login with hashed passwords (SHA256)
- Dashboard for viewing all appeals
- Update appeal status (Pending, Approved, Rejected)
- Logout functionality with secure session management

---

## 🛠️ Technologies Used

- Python 3
- Flask Framework
- MySQL (hosted on Railway)
- Rander to provide Callback link(URL)
- HTML & Bootstrap (for Admin UI)
- Africa’s Talking / Mock USSD POST Gateway

---

## ⚙️ Setup Instructions

### 1. 📦 Install Dependencies

```bash
pip install Flask Flask-MySQLdb
```

### 2. 🔧 Configuration

Update your database connection in `app.py`:

```python
app.config['MYSQL_HOST'] = 'crossover.proxy.rlwy.net'
app.config['MYSQL_USER'] = 'root'
app.config['MYSQL_PASSWORD'] = 'yourpassword'
app.config['MYSQL_DB'] = 'railway'
app.config['MYSQL_PORT'] = 29472
```

---

## 🗃️ Database Schema

### `admins`

```sql
CREATE TABLE admins (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL
);
```

### `marks`

```sql
CREATE TABLE marks (
    id INT AUTO_INCREMENT PRIMARY KEY,
    student_id VARCHAR(20),
    module_name VARCHAR(100),
    mark INT
);
```

### `appeal_status`

```sql
CREATE TABLE appeal_status (
    id INT AUTO_INCREMENT PRIMARY KEY,
    status_name VARCHAR(50)
);
```

> Sample status entries:  
> `INSERT INTO appeal_status (status_name) VALUES ('Pending'), ('Approved'), ('Rejected');`

### `appeals`

```sql
CREATE TABLE appeals (
    id INT AUTO_INCREMENT PRIMARY KEY,
    student_id VARCHAR(20),
    module_name VARCHAR(100),
    reason TEXT,
    status_id INT,
    FOREIGN KEY (status_id) REFERENCES appeal_status(id)
);
```

---

## 🖥️ Running the App

```bash
python app.py
```

- USSD endpoint: `http://localhost:5000/ussd`
- Admin login: `http://localhost:5000/admin/login`

---

## 👤 Create Admin Account

To manually add an admin user:

```python
import hashlib
hashed_password = hashlib.sha256("yourpassword".encode()).hexdigest()
# Use hashed_password to insert into the `admins` table
```

---

## 📄 License

This project is for educational purposes only. For production use, consider improving security, scalability, and error handling.

---

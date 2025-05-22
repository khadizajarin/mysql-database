

````markdown
# Flask MySQL Registration App

This is a simple Flask web application that allows users to register and log in, with data stored in an Aiven MySQL database. The app is designed to run locally and can be deployed to platforms like Render.

---

## ✨ Features

- User registration with username, password, and email.
- User login with session management.
- Password hashing using bcrypt for security.
- Data persistence in a MySQL database hosted on Aiven.

---

## ✅ Prerequisites

- Python 3.11 or later  
- Git  
- Aiven MySQL service (or any MySQL-compatible database)  
- Render account (for deployment)

---

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/mysql-database.git
cd mysql-database
````

### 2. Create a Virtual Environment

```bash
python3 -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables

Create a `.env` file in the project root with the following:

```env
MYSQL_HOST=your-aiven-mysql-host
MYSQL_PORT=your-aiven-mysql-port
MYSQL_USER=your-aiven-mysql-user
MYSQL_PASSWORD=your-aiven-mysql-password
MYSQL_DB=your-aiven-mysql-database
SECRET_KEY=your-secret-key
```

Replace the values with your Aiven MySQL credentials and a secure secret key.

Download the `aiven-ca.pem` certificate from your Aiven Console and place it in the project root directory.

---

## 🧪 Usage

### Run Locally

```bash
python3 app.py
```

* Open a browser and visit `http://localhost:5001/register` to register.
* Visit `http://localhost:5001/login` to log in.

---

## 🛠 Database Setup

Make sure the `users` table exists in your MySQL database:

```sql
USE your-database;

CREATE TABLE IF NOT EXISTS users (
    id INT(11) NOT NULL AUTO_INCREMENT,
    username VARCHAR(50) NOT NULL,
    password VARCHAR(255) NOT NULL,
    email VARCHAR(100) NOT NULL,
    PRIMARY KEY (id)
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

Connect to the database using the MySQL client with SSL:

```bash
mysql -h your-aiven-mysql-host -P your-aiven-mysql-port -u your-aiven-mysql-user -p --ssl-ca=aiven-ca.pem
```

---

## 🚀 Deployment to Render

### 1. Prepare the Repository

Commit all files, including `aiven-ca.pem`, to your GitHub repository.

```bash
git add .
git commit -m "Ready for Render deployment"
git push origin main
```

### 2. Configure Render

* Log in to [Render Dashboard](https://dashboard.render.com/)

* Create a new **Web Service**

* Connect your GitHub repository

* Configure the following:

  * **Name:** e.g., `mysql-database-l4q9`
  * **Build Command:**

    ```bash
    pip install -r requirements.txt
    ```
  * **Start Command:**

    ```bash
    gunicorn -w 4 -b 0.0.0.0:$PORT app:app
    ```
  * **Environment Variables:**

    ```env
    MYSQL_HOST=your-aiven-mysql-host
    MYSQL_PORT=your-aiven-mysql-port
    MYSQL_USER=your-aiven-mysql-user
    MYSQL_PASSWORD=your-aiven-mysql-password
    MYSQL_DB=your-aiven-mysql-database
    SECRET_KEY=your-secret-key
    ```

* Upload `aiven-ca.pem` to the project root.

* Deploy the service.

---

## 🌐 Post-Deployment

* Visit: `https://your-service-name.onrender.com/register`
* Add Render’s outbound IPs to your Aiven IP allowlist for database access.

---

## 🧩 Troubleshooting

* **502 Error:**
  Check Render logs for database connection issues. Confirm your Aiven IP allowlist and SSL certificate.

* **ModuleNotFoundError:**
  Ensure all dependencies are listed in `requirements.txt`.

* **Connection Failed:**
  Verify environment variables and the path to `aiven-ca.pem`.

---

## 📝 License

This project is **unlicensed**. Feel free to modify and use it as needed.

---

## 📬 Contact

For support, check the Render or Aiven documentation or contact your support channel.

```

```

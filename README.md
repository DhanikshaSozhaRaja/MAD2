#  Trekking Management System

A web-based Trekking Management System developed using **Flask** for the course project.

The application allows users to browse and book trekking events, staff to manage attendance, and administrators to manage treks, users, and bookings. It also includes asynchronous tasks using Celery, email notifications, Redis caching, and JSON APIs.

---

# Features

## Authentication

- User Registration
- User Login
- Logout
- Session Management
- Password Authentication using Flask-Login

---

## User Roles

The system supports three roles:

- Admin
- Staff
- User

Each role has separate dashboards and permissions.

---

# Admin Features

- Dashboard
- Add Trek
- Edit Trek
- Delete Trek
- Assign Staff to Trek
- Search Treks
- View All Bookings
- Manage Users
- Manage Feedback
- Monthly Report Email
- CSV Export Trigger
- Redis Cache Invalidation

---

# Staff Features

- Dashboard
- View Assigned Treks
- Mark Attendance
- Update Attendance

---

# User Features

- Dashboard
- Browse Open Treks
- Search Treks
- Book Trek
- Cancel Booking
- View Booking History
- Submit Feedback after Completed Treks
- Export Booking History (CSV through Email)

---

# Trek Management

Each Trek contains:

- Trek Name
- Location
- Difficulty
- Duration
- Available Slots
- Status
- Start Date
- End Date
- Assigned Staff

Date format used:

```
YYYY-MM-DD
```

Dates are stored as strings and converted using:

```python
datetime.strptime(trek.start_date, "%Y-%m-%d").date()
```

---

# Booking Workflow

Users can:

- View Available Treks
- Book Trek
- Cancel Booking

Features include:

- Duplicate booking prevention
- Slot availability checking
- Automatic slot reduction
- Automatic slot restoration
- Booking history

Booking statuses:

- Pending
- Confirmed
- Cancelled
- Rejected

---

# Attendance

Staff members can:

- Mark Attendance
- Update Attendance

Attendance is visible in booking history.

---

# Feedback System

Users can submit feedback only when:

- Trek is Completed
- Booking Status is Confirmed
- Feedback has not already been submitted

Features:

- Rating (1–5)
- Comments
- Average rating shown on trek listings

---

# Search

Search functionality is available for:

- Treks
- Admin Trek Management
- User Trek Browsing

---

# JSON APIs

REST APIs are implemented for project requirements.

---

# Email Features

Implemented using Flask-Mail.

Includes:

- Daily Trek Reminder Emails
- Monthly Admin Report
- Booking History CSV Export

---

# Celery Tasks

Background tasks implemented using Celery and Redis.

Tasks include:

### Daily Reminder

- Sends reminders for confirmed bookings before trek start date.

### Monthly Admin Report

Includes:

- Total Treks
- Completed Treks
- Total Participants
- Most Popular Trek
- Booking Statistics

### CSV Export

Users can export booking history.

CSV contains:

- Booking ID
- Trek Name
- Location
- Start Date
- End Date
- Duration
- Booking Date
- Booking Status
- Attendance

The CSV is generated asynchronously and emailed to the user.

---

# Redis Caching

Implemented using Flask-Caching.

Cached Page:

- Open Trek Listing

Cache timeout:

```
5 Minutes
```

Cache invalidates after:

- Add Trek
- Edit Trek
- Delete Trek
- Book Trek
- Cancel Booking

---

# Technologies Used

- Python
- Flask
- SQLite
- SQLAlchemy
- Flask-Login
- Jinja2
- Bootstrap 5
- Celery
- Redis
- Flask-Mail
- Flask-Caching
- Docker Desktop

---

# Project Structure

```
trekking_management/
│
├── app.py
├── config.py
├── celery_config.py
├── celery_worker.py
├── tasks.py
│
├── models/
│   └── database.py
│
├── routes/
│   ├── auth.py
│   ├── admin.py
│   ├── staff.py
│   └── user.py
│
├── templates/
│
├── static/
│
├── instance/
│   └── trekking.db
│
├── requirements.txt
│
└── README.md
```

---

# Installation

## 1. Clone Repository

```bash
git clone <repository-url>
```

---

## 2. Create Virtual Environment

```bash
python -m venv venv
```

Activate:

Windows

```bash
venv\Scripts\activate
```

Linux/Mac

```bash
source venv/bin/activate
```

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

## 4. Start Redis

Using Docker:

```bash
docker run -d -p 6379:6379 redis
```

---

## 5. Run Celery Worker

```bash
celery -A celery_worker.celery worker --pool=solo --loglevel=info
```

---

## 6. Run Celery Beat

```bash
celery -A celery_worker.celery beat --loglevel=info
```

---

## 7. Run Flask Application

```bash
python app.py
```

Open:

```
http://127.0.0.1:5000
```

---

# Default Roles

The system supports:

- Admin
- Staff
- User

Admin can manage all system modules.

---



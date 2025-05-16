# 🏥 Clinic Booking System (MySQL Database)

This project implements a full-featured **relational database schema** for a clinic booking system using **MySQL**. It supports user authentication, appointment scheduling, doctor-patient management, and service tracking.

---

## 📌 Features

- Role-based `Users` system (Admin, Doctor, Receptionist, Patient)
- Appointment scheduling between doctors and patients
- Department-based doctor organization
- Prescription management per appointment
- Support for multiple services per appointment (lab tests, consultations, etc.)

---

## 🗃️ Database Schema Overview

### 📦 Tables

| Table Name              | Description                                              |
|-------------------------|----------------------------------------------------------|
| `Users`                 | Stores login credentials and roles                       |
| `Departments`           | Hospital departments (e.g., Cardiology, Pediatrics)      |
| `Doctors`               | Doctor info, linked to `Users` and `Departments`         |
| `Patients`              | Patient info, linked to `Users`                          |
| `Appointments`          | Doctor-patient meeting records                           |
| `Services`              | List of offered medical services                         |
| `Appointment_Services`  | Join table linking appointments to services (M:N)        |
| `Prescriptions`         | Medication details for a specific appointment            |

---

## 🧩 Relationships

- `Users` → `Doctors` and `Patients` (1:1)
- `Departments` → `Doctors` (1:N)
- `Patients` → `Appointments` (1:N)
- `Doctors` → `Appointments` (1:N)
- `Appointments` → `Prescriptions` (1:1)
- `Appointments` ↔ `Services` (M:N via `Appointment_Services`)

---

## 🛠️ How to Use
1. Open the `clinic_booking_system.sql` file in your MySQL tool (VS Code, MySQL Workbench, or any MySQL client).
2. Connect to your MySQL server and select a target database.
3. Run the SQL script to create all tables and relationships.

---

## ✅ Sample Usage

```sql
-- Get all appointments for a doctor
SELECT a.appointment_date, p.full_name AS patient
FROM Appointments a
JOIN Patients p ON a.patient_id = p.patient_id
WHERE a.doctor_id = 1;

-- List services used in an appointment
SELECT s.name
FROM Services s
JOIN Appointment_Services aps ON s.service_id = aps.service_id
WHERE aps.appointment_id = 10

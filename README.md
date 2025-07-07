# 🔐 Server-Client Authentication Framework

## 📖 Overview

This project implements a **secure, AI-enhanced server-client authentication system** featuring phishing detection, multi-factor authentication, device fingerprinting, geolocation verification, and time-based login validation. It integrates an AI model with **71.25% accuracy** to classify URLs as phishing or legitimate, and enforces advanced security measures during login processes.

---

## ⚙️ Features

✅ AI-powered URL phishing detection  
✅ Session token generation and validation  
✅ Multi-factor authentication (username, password, token)  
✅ Device fingerprinting (OS, BIOS UUID, motherboard ID, Wi-Fi MAC)  
✅ Geolocation detection via IP  
✅ Time-based login validation  
✅ Email notifications for suspicious activity  
✅ Secure logging of all authentication attempts

---

## 🖥️ Server Process

### 1️⃣ Start Server
- Initializes a TCP socket server listening on port **8000** for client connections.

### 2️⃣ AI URL Verification
- Upon receiving a URL, the AI model predicts:
  - **Legitimate** → Proceeds to token generation.
  - **Phishing** → Terminates connection.

### 3️⃣ Session Token Generation
- If the URL is legitimate:
  - Generates a unique session token.
  - Sends the token to the client.
  - Validates token upon client’s response.

### 4️⃣ Authentication Workflow
- Client submits:
  - **Username**
  - **Password**
  - **Device Info**
  - **Device Fingerprint**
  - **Geolocation**
  
- Server verifies credentials using an Excel database:
  - On success:
    - Validates **device fingerprint**.
    - Validates **login time** against allowed login windows.
    - Validates **location**.
  - On mismatches:
    - Logs anomalies.
    - Sends **email notifications** to the user with device, time, and location details.

- All authentication attempts are recorded in a `logs.csv` file.

---

## 📲 Client Process

### 1️⃣ Connect to Server
- Establishes a connection to the server’s IP and port.

### 2️⃣ URL Submission & Classification
- Client inputs a URL.
- Receives classification result and token if URL is legitimate.

### 3️⃣ Multi-Factor Authentication
- User provides:
  - Session token.
  - Username & Password (3 attempts max).
- Sends:
  - OS and hardware info.
  - Device fingerprint.
  - Geolocation via `ipinfo.io`.

### 4️⃣ Result Handling
- On success:
  - Receives authentication confirmation.
- On failure:
  - Receives appropriate termination or retry prompts.

---

## 🔒 Security Modules

- **AI-powered Phishing Detection**: Uses pre-trained ML model to classify URLs.
- **Unique Token Management**: Session tokens generated with UUID, tracked for uniqueness.
- **Device Fingerprinting**: Captures:
  - OS details
  - BIOS UUID
  - Motherboard ID
  - Wi-Fi MAC address
- **Geolocation Detection**: Fetches IP-based location using the `ipinfo.io` API.
- **Time-based Validation**: Confirms login is within allowed time windows per user profile.
- **Email Notifications**: Sends alerts to users on suspicious login activity.
- **Centralized Logging**: All attempts recorded with full context and result status.

---

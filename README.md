# 🔐 ASP.NET MVC Login System with Malicious Input Detection & Google Authenticator 2FA

This project demonstrates a secure login system in ASP.NET MVC using:

- ✅ Malicious input detection via a separate Web API service
- ✅ Google Authenticator-based 2-Factor Authentication (2FA)

---

## 📁 Projects Overview

### 1. **SecurityDetectionService** (Web API)
- ASP.NET Web API (.NET Framework)
- Exposes an endpoint: `POST /api/security/check`
- Detects malicious inputs like:
  - SQL Injection (`DROP TABLE`, `SELECT *`)
  - XSS (`<script>`)
  - OS Commands (`rm -rf`, etc.)

### 2. **LoginApp** (MVC Web App)
- ASP.NET MVC (.NET Framework)
- Handles login UI, authentication logic, and 2FA
- Integrates with the API to validate input
- Uses `GoogleAuthenticator.dll` (Brandon Potter's library) for 2FA

---

## 🔗 Integration Flow

1. **User submits login form**
2. **LoginApp** calls **SecurityDetectionService** to check if the input contains malicious patterns.
3. If input is clean:
   - Checks if credentials are valid (`usman / 1234`)
   - Redirects to 2FA step
4. On 2FA step:
   - A QR code and secret key are shown
   - User scans with Google Authenticator app
   - Enters the 6-digit TOTP code
5. If valid → Redirects to success page ✅

---

## 🚀 How to Run

### Prerequisites:
- Visual Studio
- .NET Framework
- Curl (for testing API if needed)

### Step-by-Step

1. **Open both projects in one solution in Visual Studio**
2. Set **multiple startup projects**:
   - Right-click solution → Properties → Startup Projects
   - Select "Multiple Startup Projects" and set both to "Start"
3. Hit `F5` to run both:
   - API: `https://localhost:44346/api/security/check`
   - Web App: `https://localhost:44390/Login`
4. Try logging in:
   - Malicious input → error
   - Valid input → 2FA prompt

---

## 🔐 2FA Details

- Secret key is generated per session (can be replaced with DB-stored value)
- QR code is displayed to scan with the Google Authenticator app
- 2FA token is validated using `GoogleAuthenticator.dll`

---

## 📦 Libraries Used

- **Google.Authenticator** (`GoogleAuthenticator.dll`)
- **Newtonsoft.Json** for JSON serialization
- **ASP.NET MVC + Web API** (.NET Framework)

---

## ✅ Example Credentials

- **Username:** `usman`
- **Password:** `1234`

---

## 📌 Notes

- The secret key for 2FA is currently hardcoded (`"MYSECRETKEY123456"`) for testing.
- In production, store user secrets securely (DB or encrypted storage).
- You can extend detection rules in the Security API as needed.

---

© 2025 - Project by [Your Name]

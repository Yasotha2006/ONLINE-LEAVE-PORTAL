# Online Leave Portal

A **Flask-based leave management system** with employee leave requests, manager approvals, and calendar visualization.

---

## Overview

This application provides a complete leave management solution:

- Employees can request leave (sick, vacation, personal)
- Managers can approve or reject leave requests
- Leave balances are tracked automatically
- Calendar view shows approved leaves
- Authentication powered by **Replit Auth (OIDC)**

---

## Recent Changes
**October 16, 2025**

- Initial implementation of leave portal
- Integrated Replit Auth for user authentication
- Created database models for users, leave requests, and balances
- Implemented employee and manager dashboards
- Added calendar view with FullCalendar.js
- Configured Flask workflow on port 5000

---

## Project Architecture

### Backend (Flask/Python)
- `app.py`: Flask app initialization with SQLAlchemy
- `models.py`: Database models (User, OAuth, LeaveBalance, LeaveRequest)
- `replit_auth.py`: Replit Auth/OIDC integration via Flask-Dance
- `routes.py`: Application routes and business logic
- `main.py`: Application entry point

### Frontend (HTML/Bootstrap/JavaScript)
- `templates/`: Jinja2 templates with Bootstrap 5 styling
  - Landing page for unauthenticated users
  - Employee dashboard with leave balance and request history
  - Leave request form with validation
  - Manager dashboard for approvals
  - Calendar view with FullCalendar.js
- `static/`: Static assets (currently minimal, using CDNs)

---

## Database Schema
- **users**: User authentication and profile data (managed by Replit Auth)  
- **oauth**: OAuth tokens and session management (for Replit Auth)  
- **leave_balances**: Employee leave allocations  
  - sick: 10, vacation: 15, personal: 5  
- **leave_requests**: Leave request records with status tracking  

---

## Key Features
- **Authentication**: Replit Auth (Google, GitHub, X, Apple, email)
- **Leave Request**: Submit requests with date range, type, and reason
- **Leave Balance**: Automatic tracking and deduction on approval
- **Manager Workflow**: Approve/reject requests with comments
- **Calendar View**: Visual representation of approved leaves
- **Role Switching**: Demo feature to switch between employee and manager roles

---

## Security Considerations

- **Authentication Security**
  - Replit Auth (OIDC/OAuth2) with PKCE
  - Session tokens stored server-side (PostgreSQL)
  - Full JWT signature verification using PyJWT with JWKS
  - Validates JWT signature (RS256), issuer, audience, expiration
  - Comprehensive error handling for expired/invalid tokens

- **Best Practices**
  - Environment variables for sensitive configs (`SESSION_SECRET`, `DATABASE_URL`)
  - Server-side validation of all leave requests
  - Role-based access control for manager functions
  - HTTPS enforcement via ProxyFix middleware

---

## Environment Variables

**Required**
- `DATABASE_URL`: PostgreSQL connection string (auto-configured)
- `SESSION_SECRET`: Flask session secret (auto-configured)
- `REPL_ID`: Replit workspace identifier (auto-configured)

**Optional**
- `ISSUER_URL`: OIDC issuer URL (defaults to `https://replit.com/oidc`)

  
  **Future Enhancements**

**The project roadmap includes:**

-**Email notifications:** Automatically notify employees and managers about leave approvals/rejections

-**Multi-level approval workflows**: Support for departmental heads or HR approvals

-**Admin panel:** Manage company leave policies, employee allocations, and system settings

-**Leave balance carry-forward rules:** Automatically handle unused leave from previous years

-**Holiday calendar integration:** Show public and company holidays in the calendar view

-**Analytics dashboard**: Track leave trends, department usage, and employee attendance

-**Mobile-friendly UI:** Improve responsiveness for mobile and tablet devices

-**Reporting tools:** Export leave reports in CSV or PDF format

-**Enhanced security**: Two-factor authentication and audit logs

---

## Running the Application

Run the Flask server via:

```bash
python main.py

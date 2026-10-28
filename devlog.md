# 2026-10-28 — Requirements Analysis & Core Architecture

**Did:** Overcame initial ambiguity in the system requirements, establishing the core user roles, ticket lifecycle, access control rules, and security baselines. Used Claude as a Tutor modular tool and Gemini to help reformat devlog.

**Decided:**
* **Authentication & Authorization:** Planned a unified user model with a `role` field (user, staff, admin) to avoid maintaining duplicate authentication pipelines.
* **Brute-Force Protection:** Used `express-rate-limit` to restrict requests per IP address (mitigating campus-wide Wi-Fi DoS risks) combined with per-account exponential delays on failed PIN attempts rather than hard account lockouts, balancing security against denial-of-service risks.
* **Ticket Lifecycle & Auto-Close:** 
  * Tickets marked as resolved automatically transition to closed after 3 days of inactivity.
  * If a user replies within that 3-day window, the ticket automatically reopens to "In Progress".
  * The dashboard distinguishes between user-closed tickets ("no longer needed") and staff-resolved/auto-closed tickets.
  * Staff can manually roll back a resolved ticket to "In Progress" if a fix fails.
* **Access Control & Error Handling:** Requests for non-existent ticket IDs *or* valid tickets belonging to another user both return a standard `404 Not Found` response to prevent IDOR enumeration attacks.

**Unsure / to revisit:**
* Fine-tuning the exact exponential backoff timing coefficients for login failures.

**Evidence:**
* Git Commit Hash: 

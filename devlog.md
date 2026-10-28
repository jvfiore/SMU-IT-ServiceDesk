# 2026-10-28 — Requirements Analysis & Core Architecture

**Did:** Overcame initial ambiguity in the system requirements, establishing the core user roles, ticket lifecycle, access control rules, and security baselines. Used Claude as a Tutor modular tool and Gemini to help reformat devlog.

**Decided:**
* **Authentication & Authorization:** Planned a unified user model with a `role` field (user, staff) to avoid maintaining duplicate authentication pipelines.
* **Brute-Force Protection:** Planned `express-rate-limit` to restrict requests per IP address (mitigating campus-wide Wi-Fi DoS risks) combined with per-account exponential delays on failed password attempts rather than hard account lockouts, balancing security against denial-of-service risks.
* **Ticket Lifecycle & Auto-Close:** 
  * Tickets marked as resolved automatically transition to closed after 3 days of inactivity.
  * If a user replies within that 3-day window using a dedicated "Still Broken" button, the ticket automatically reopens to "In Progress" (preventing casual "thanks!" replies from reopening tickets).
  * The dashboard distinguishes between user-closed tickets ("no longer needed") and staff-resolved/auto-closed tickets.
  * Staff can manually roll back a resolved ticket to "In Progress" if a fix fails.
* **Access Control & Error Handling:** Requests for non-existent ticket IDs *or* valid tickets belonging to another user both return a standard `404 Not Found` response to prevent IDOR enumeration attacks.

**Unsure / to revisit:**
* Fine-tuning the exact exponential backoff timing coefficients for login failures.

**Evidence:**
* State Diagram: * [C:\Users\josep\OneDrive\Documents\GitHub\SMU-IT-ServiceDesk\docs\State Diagram.drawio.png]
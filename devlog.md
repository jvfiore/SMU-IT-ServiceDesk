## 2026-10-28 — Used Claude Opus 5.5 as a tutor for Requirements analysis
Did: Overviewed all documents to come up with a base idea of requirements (Decided on first set of roles, lifecycle, access rule and security brainstorming)

Decided: 
- Support Staff and Users operate under different IDs and Passwords (Users create their own ID/Password to login with, staff are provided with a developer made private ID and PIN for staff login) (Limit login attempts to counter attacking PIN pull scripts: Locked Out after 5 incorrect attempts)(Considered one shared login logic with a role field but rejected it: twice the code to secure and test)
- How tickets close (A ticket can either be closed via being marked as resolved by staff, or users themselves can close tickets if they no longer need help (marked closed, if the problem comes back they must make a new ticket, whereas staff can change a ticket from resolved back to in prog if fix didn't finalize)(Tickets automatically move from resolved --> closed after 3 days)
- When user attempts to access tickets from ID that isn't there draw 404 not found error, this prevents revealing the existence of ticket to potential attacker

Unsure / to revisit: 
- How Tickets Close

Evidence: 

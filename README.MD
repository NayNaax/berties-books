# Berties Books

Sample code for Dynamic Web Applications module.

Uses node.js with Express and EJS.

To install and run:

1. Install dependencies

```pwsh
npm install
```

2. Configure environment variables (dotenv)

Copy `.env.example` to `.env` and adjust values:

```pwsh
Copy-Item .env.example .env
```

Required variables:

-   DB_HOST
-   DB_USER
-   DB_PASSWORD
-   DB_NAME

3. Start the app

```pwsh
npm start
```

Note: `.env` is git-ignored; never commit secrets.

## dotenv

This project uses the `dotenv` module to keep database credentials out of source code:

-   Load: `require('dotenv').config()` at the top of `index.js`.
-   Configure: create a `.env` file (based on `.env.example`) with `DB_HOST`, `DB_USER`, `DB_PASSWORD`, `DB_NAME`.
-   Use: `index.js` reads these via `process.env` when creating the MySQL pool.
-   Safety: `.env` is listed in `.gitignore`, so secrets are not committed.

Tip: For different environments, keep separate `.env` files locally (e.g., `.env.development`), but never push them to Git.

## audit

All login attempts (successes and failures) are recorded in the `login_attempts` table for auditing purposes:

- Each attempt logs the username, result (success/failure), reason, and timestamp.
- The `/users/loggedin` route inserts a record for every login attempt.
- View the full audit history at `/users/audit` (renders `views/audit.ejs`).
- The audit table shows ID, timestamp, username, success, and reason for each attempt.

This helps track authentication activity and can be used for security monitoring or troubleshooting.

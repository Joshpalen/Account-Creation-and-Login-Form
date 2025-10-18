# Account Creation and Login Form (Frontend)

A small, dependency‑free frontend (HTML/CSS/JS) for the Account Auth Backend. It provides user flows for registration, login, email verification, password reset, and optional TOTP-based 2FA.

Features
- Sign up with strong‑password guidance
- Login with JWT stored in localStorage
- Email verification (paste token or full link)
- Password reset request flow
- Optional 2FA (TOTP) setup/verify/disable, via QR code
- Minimal UI with zero build tooling — serve as static files

Requirements
- A running backend API (the repo named “Account‑Creation‑and‑Login‑Form‑Backend”).
- CORS must allow the frontend origin if hosting separately.

Quick Start (same origin)
1) Place these files behind the backend’s static hosting, or open `index.html` with a static server (e.g., `npx serve`).
2) Backend default endpoints are `/auth/*` and `/totp/*` on the same origin, which the frontend uses by default.

Quick Start (separate origin)
- In `index.html`, before `script.js`, set the backend base URL:

```html
<script>
  window.API_BASE_URL = 'https://your-backend-host';
</script>
<script src="script.js"></script>
```

Security Notes
- The backend handles hashing, tokens, and 2FA verification. The frontend never stores passwords beyond the request body.
- Avoid serving this over plain HTTP in production.

Available Routes (backend)
- POST `/auth/register` — create account
- GET `/auth/verify?token=...` — verify email (token from email link)
- POST `/auth/login` — obtain JWT
- POST `/auth/password-reset` — send reset email
- POST `/auth/password-reset/confirm` — set new password (with token)
- POST `/totp/setup` — start 2FA and receive an `otpauth://` URL
- POST `/totp/verify` — enable 2FA by verifying code
- POST `/totp/disable` — disable 2FA

Development Tips
- Use a simple static server to avoid CORS for `file://` URLs: `npx serve .` or VS Code Live Server.
- If you host separately, set `window.API_BASE_URL` and configure backend CORS.

License
MIT

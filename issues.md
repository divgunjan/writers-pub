## Issue: Login form pre-fills shared credentials

**Title**: Sign-in page exposes a prefilled email and password

**Description**: The login form is initialized with demo credentials in the UI, which means the sign-in page shows a real email and password before the user types anything. That is a security and privacy issue because credentials are visible by default and can be reused without the user intentionally entering them.

**Why this matters**:
- It exposes credentials in the browser UI.
- It can lead to accidental login with shared/demo accounts.
- If the same credentials exist in a deployed environment, it becomes a real security risk.

**Relevant files**:
- [web/src/app/login/page.tsx](web/src/app/login/page.tsx)
- [server/src/db/seed.ts](server/src/db/seed.ts)

**My approach before patching and creating a PR**:
1. Confirm the source of the prefill in the login component and the matching seeded account on the backend.
2. Remove hardcoded default values from the login form so both fields start empty.
3. Check whether any demo login flow is needed; if yes, move it behind an explicit dev-only action instead of prefilled inputs.
4. Keep browser-friendly attributes like `autoComplete="username"` and `autoComplete="current-password"` without exposing values.
5. Verify the sign-in page no longer shows credentials on load, then open a small PR with the UI fix and any seed cleanup needed.

**Expected fix outcome**:
- No credentials are visible on initial load.
- Users must type or autofill their own credentials.
- Demo credentials, if kept, are isolated to local/dev-only workflows.


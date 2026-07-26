---
name: Onboard a user to eFront
description: Create a user in eFront, add them to a branch, and activate the account.
api: openapi/epignosis-talentlms-efront-talentcards-efront-openapi-original.json
operations:
  - POST /User
  - PUT /Branch/{Id}/AddUser
  - PUT /User/{Id}/Activate
---

# Onboard a user to eFront

Use the eFront REST API (`https://{installation}/API/v1.0`). Authenticate with your API
key as the HTTP Basic **username** and a **blank password**. All requests must be HTTPS.

## Steps

1. **Create the user** — `POST /User` with the `createUser` body (login, email, name,
   surname, user type). The response returns the new user `id`.
2. **Assign to a branch** (optional) — `PUT /Branch/{Id}/AddUser` with the branch `Id`
   and the user id, so the user lands in the right sub-portal.
3. **Activate the account** — `PUT /User/{Id}/Activate` to make the user active (use
   `PUT /User/{Id}/Deactivate` to reverse).

## Rules

- Auth: API-key Basic auth (key = username, blank password); see
  `authentication/epignosis-talentlms-efront-talentcards-authentication.yml`.
- Errors: JSON `error` object with `code`/`message`/`reason`; 400 bad request, 404 not
  found. See `errors/epignosis-talentlms-efront-talentcards-efront-problem-types.yml`.
- No idempotency key — do not blindly retry `POST /User`; check with
  `GET /Users/{eMailAddress}` first to avoid duplicates.

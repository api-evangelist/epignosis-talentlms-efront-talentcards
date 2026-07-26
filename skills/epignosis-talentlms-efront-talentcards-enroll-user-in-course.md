---
name: Enroll a user in a course and track progress
description: Find a course in eFront, enroll a user, then read their progress.
api: openapi/epignosis-talentlms-efront-talentcards-efront-openapi-original.json
operations:
  - GET /Courses
  - PUT /Course/{Id}/AddUser
  - GET /Course/{CourseId}/UserProgress/{UserId}
---

# Enroll a user in a course and track progress

Use the eFront REST API (`https://{installation}/API/v1.0`) with API-key HTTP Basic auth
(key = username, blank password), over HTTPS.

## Steps

1. **Locate the course** — `GET /Courses` to list courses, or `GET /Course/{Id}` for one
   course, and capture the course `Id`.
2. **Enroll the user** — `PUT /Course/{Id}/AddUser` with the course `Id` and the user id.
   To remove them later use `PUT /Course/{Id}/RemoveUser`.
3. **Track progress** — `GET /Course/{CourseId}/UserProgress/{UserId}` to read completion,
   and `GET /CourseUserStatus/{CourseId},{UserId}` for status; test attempts are at
   `GET /CourseUserTestAttempts/{CourseId},{UserId}`.

## Rules

- Auth + errors + conventions as in the eFront error/authentication/conventions
  artifacts in this repo.
- No pagination contract on `GET /Courses`; filter client-side for large catalogs.
- Writes are not idempotent; verify enrollment before re-issuing `PUT /Course/{Id}/AddUser`.

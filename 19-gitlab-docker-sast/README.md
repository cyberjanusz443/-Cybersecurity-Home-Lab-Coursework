# 19 — Self-Hosted GitLab + Docker + SAST

Full DevSecOps exercise: deployed a private GitLab instance in Docker,
configured the complete Git workflow (clone, branch, merge request, merge),
and performed Static Application Security Testing (SAST) on a vulnerable
Flask application.

## What I did

### Junior tier — Local Git fundamentals
- Initialized a local Git repository on Ubuntu
- Created a notes folder with test content
- Practiced the basic Git workflow: `add`, `commit`, push to local origin
- Verified file synchronization between working tree and repository

### Medium tier — Self-hosted GitLab CE
- Deployed **GitLab Community Edition** in Docker:
  ```bash
  docker run -d --name gitlab gitlab/gitlab-ce:latest
  # with port mappings: 80:80, 443:443, 22:22
  ```
- Container status: `healthy`, exposing HTTP/HTTPS web UI and SSH for Git
- Retrieved the initial root password from `/etc/gitlab/initial_root_password`
  inside the container
- Logged into GitLab web UI as `root`, created a personal access token

### GitFlow workflow end-to-end
- Created new project `moj-projekt` in GitLab
- **From Windows side:**
  - Configured Git client with name, email, and authentication token
  - Cloned the GitLab repository
- Practiced branching workflow:
  - Created new branch `nowa-galaz`
  - Made commits with notes
  - Pushed branch to GitLab
  - Opened **Merge Request** in GitLab web UI
  - Reviewed and approved the merge request
  - Merged into `main` (merge commit hash `6ee950fd`)
  - Source branch automatically deleted after merge

### Static Application Security Testing (SAST) — Flask application
Reviewed a Flask web application for security vulnerabilities through
static code analysis. Identified critical issues:

- **DEBUG mode enabled in production code** — Flask's debug mode exposes
  an interactive Python debugger via web UI on errors, allowing
  **remote code execution** to anyone who can trigger an exception
- **Hardcoded SECRET_KEY** — session signing key visible in source,
  enabling session forgery if code is leaked
- **Weak password hashing (raw SHA-256)** — no salt, no key derivation
  function (bcrypt, scrypt, argon2). Vulnerable to rainbow tables.
- **SQL injection risk** — string-formatted queries instead of parameterized
- **No CSRF protection** on state-changing endpoints
- **Verbose error messages** disclosing stack traces and database structure

## Key screenshots
- `junior_Utworzenie_Repo_na_Ubuntu.jpg` — Local Git repository initialization
- `junior_Operacja_PUSH.jpg` — First push to local origin
- `medium_Pobranie_Hasla_ROOT.jpg` — Retrieving GitLab root password
- `medium_Logowanie_GitLAB.jpg` — Successful root login to web UI
- `medium_status_GitLAB.jpg` — `docker ps` showing healthy GitLab container
- `medium_KonfiguracjaGit_Windows.jpg` — Git client configuration on Windows
- `medium_Logowanie_GITLAB_Windows.jpg` — Cross-platform Git authentication
- `medium_Nowa_Galaz_Push_Notatki.jpg` — Pushing new branch with notes
- `medium_PUSH_notatki_Do_GITLAB.jpg` — Branch push successful
- `medium_Akceptacja_merge_request.jpg` — Merge request approved and merged

## Files
- `GitLAB.pdf` — full GitLab + Git workflow documentation
- `RAPORT_BEZPIECZENSTWA_-_APLIKACJA_FLASK.pdf` — SAST report on the
  vulnerable Flask application with findings and remediation recommendations

## Takeaway
**DevSecOps shifts security "left" — closer to the developer, earlier in
the SDLC.** This exercise touched all three legs:

1. **Dev** — Git workflow (the universal version control standard)
2. **Sec** — SAST identifies vulnerabilities **before** code reaches production
3. **Ops** — Docker for repeatable, ephemeral infrastructure

**Why GitLab matters for a security analyst:**
- Modern attack investigation often starts with "who changed what, when?"
  — and that's a `git log` query
- Many security teams operate as **infrastructure-as-code shops** — your
  firewall rules, SIEM detections, IAM policies are all in Git
- A compromised CI/CD pipeline can deploy malicious code to production
  faster than any incident response can react — protecting the SDLC
  is core security work

**Why SAST matters:** every vulnerability found in code review is a
vulnerability that **never reaches production**. SAST tools (Semgrep,
SonarQube, GitLab SAST) integrated into CI/CD catch the obvious bugs
automatically, freeing human review for the subtle ones.

The Flask application I audited had **every classic Python web mistake**
in one place — it was a great teaching artifact, but the lessons apply
to every web framework: never deploy debug mode, never hardcode secrets,
never roll your own crypto, always parameterize queries.

For my career: even SOC L1 analysts in modern shops are expected to
read code (Bash, Python, PowerShell) — knowing how SAST findings translate
to runtime behavior is a direct advantage.

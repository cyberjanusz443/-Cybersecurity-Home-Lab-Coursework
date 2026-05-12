# 08 — MFA & Password Managers

Identity and authentication exercise covering modern access control:
multi-factor authentication, password managers, federated identity,
and single sign-on (SSO).

## What I did
- Documented the operational differences between MFA factor categories:
  - **Something you know** — passwords, PINs
  - **Something you have** — TOTP apps (Google Authenticator, Aegis),
    hardware tokens (YubiKey, FIDO2 security keys), SMS (weakest, SIM-swap risk)
  - **Something you are** — biometrics (fingerprint, FaceID)
- Compared **password manager architectures**:
  - Cloud-synced (Bitwarden, 1Password) vs. local-only (KeePassXC)
  - Zero-knowledge encryption model — master password never leaves the device
  - Threat model: device compromise vs. provider compromise vs. master password loss
- Studied **federated identity** protocols:
  - **OAuth 2.0** — delegated authorization (e.g., "Sign in with Google")
  - **SAML 2.0** — enterprise SSO between identity provider (IdP) and service provider (SP)
  - **OpenID Connect** — authentication layer on top of OAuth 2.0
- Mapped where each factor sits in the **NIST 800-63B** Authenticator Assurance Levels (AAL)

## Files
- `MFA i menedżer haseł.pdf` — full written assignment covering all topics above

## Takeaway
MFA is not optional in 2026 — it's the single most effective control
against credential-based attacks (phishing, password reuse, database leaks).
But **not all MFA is equal**:
- **SMS-based 2FA** can be bypassed via SIM swapping
- **TOTP apps** are phishable in real-time (attacker proxies the login page)
- **FIDO2 / WebAuthn** are phishing-resistant by design — the browser
  cryptographically verifies the domain before responding

For a security analyst's day-to-day: when investigating account compromise,
the first question is always "what authentication factors were used?" — and
that question's answer determines half the incident severity.

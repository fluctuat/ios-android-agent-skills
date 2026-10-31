---
name: test-account-automation
description: Set up reusable test personas and secret-backed native sign-in helpers when manual credential entry slows QA or creates leaks.
license: CC0-1.0
---

# Reusable test accounts without credentials in the agent transcript

Use when repeated sign-ins, identity confusion or secret handling are slowing
native QA. The useful artifact is an alias-driven sign-in operation. The agent
should select a persona and observe a result without receiving its password.

## Separate the registry from the secret store

Maintain one private account registry mapping persona alias to environment,
app account, role, store-account alias, device-profile alias, initial entitlement
state and freshness. Store secret references rather than passwords. Read only
the row needed for the task. Keep the registry outside the shared collection.

Use an OS credential store (for example Keychain or Credential Manager), a
password manager integration, or a managed secret store for values. A private file
is a fallback only when the project's threat model and access controls permit
it; `.gitignore` alone does not protect backups, logs or process output.
A PIN, recovery code, attestation token and password are all sensitive inputs.
Do not turn a convenient test PIN into a hardcoded shared fixture secret.

## Put secret resolution inside the helper

The helper takes an alias, destination and expected app/environment. It:

1. Resolves approved private metadata and verifies the target app/profile.
2. Retrieves the secret internally, with shell tracing and value logging off.
3. Identifies the visible credential controls by fresh semantic identifiers.
4. Supplies values through a transport whose logging and persistence have been
   checked, submits, and waits for the expected stable landing state.
5. Reports alias, environment, elapsed time and a safe failure category only.

Do not put the secret in CLI arguments, a saved replay, a screenshot caption,
chat, or a temporary script. Environment variables are not automatically safe:
child-process diagnostics and crash reporters may capture them. Prefer an
in-process secret-aware input interface; if the available tool records values,
keep secure entry manual rather than claiming the automation is secret-safe.
Treat session cookies, refresh/access tokens and saved authenticated tool state
as sensitive too. A reusable signed-in session is useful, but its storage is not
a shareable test artifact. Developer-login prefill, when used, belongs to an
isolated development build and must not become a release login bypass.

If an earlier run exposed a real secret, stop further use of that recording path
and identify the affected artifacts without quoting values. Arrange authorized
revocation/rotation and artifact sanitization with the credential owner; restrict
access while preserving any required incident evidence. Do not silently rotate a
shared account or treat deleting one local log as complete remediation.

Read [the helper contract](references/helper-contract.md) for a concrete registry
shape and a harmless-marker leakage check. It is a design example, not a shipped
CLI or permission to provision accounts.

## Choose the persona to match the claim

| Test | Reusable fixture | Why another fixture may be necessary |
|---|---|---|
| Layout after login | Already signed-in synthetic user | No need to reauthenticate for every screenshot |
| First-time onboarding | Deliberately fresh app account | Reinstall does not remove server onboarding state |
| First purchase or trial eligibility | Known app/store pairing with documented history | A fresh app account does not reset store history |
| Restore | Established purchaser, same intended owner | Clearing history would destroy the thing being tested |
| Cross-platform ownership | Explicitly paired platforms | Ordinary independent platform tests should not contaminate each other |

Reuse a session until the claim requires a fresh one. Refresh the registry after
an authorized reset or role change. Never reset personal subscriptions or
transfer a transaction between accounts as test cleanup.

## Stop at real system confirmation

App-password entry and OS/store confirmation are different. A required passcode,
biometric check or secure system sheet can remain a human step. Identify that
step before the run and keep the session ready. Do not disable a person's device
security or type a secret at an unidentified coordinate to achieve automation.

Completion means the correct persona reaches its expected native screen and
secret handling has been checked. “Account exists” and “credentials retrieved”
are not completed sign-in. Preserve one usable recipe, not a new account guide
for each run.

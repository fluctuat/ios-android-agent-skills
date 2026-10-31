# Example account registry and helper behavior

Fictional metadata shape; this is not an executable configuration format:

```yaml
alias: checkout-ios-fresh
app_environment: staging
app_identity: development-app
app_account_ref: private-account-record
password_ref: credential-store-item
store_account_alias: ios-test-fresh
device_profile_alias: qa-profile
role: ordinary-customer
expected_state: signed-in-free
history: never-purchased
last_verified: record-at-runtime
```

The actual record is private. The shared repository contains neither its real
values nor the locations of production credentials. A machine-local adapter
resolves the references; moving to another machine requires its own authorized
secret provisioning, not copying someone's personal credential store.

## Proposed helper interface

This is illustrative syntax for a project's own helper, not a command supplied
by this collection:

```text
qa sign-in --persona checkout-ios-fresh --destination qa-phone
```

Expected safe result:

```text
persona=checkout-ios-fresh environment=staging
result=landed expected_screen=home
secret_transport_check=passed-for-recorded-tool-configuration
```

The last field points to the completed marker check and its tool/recording
configuration. It is not a guarantee about every host or future run.
Useful failure categories include wrong-app, missing-secret, unidentified-field,
provider-rejected, attestation-rejected, setup-required and landing-timeout. Never
include the credential or provider token in the diagnostic message.

## Check the tool before trusting it with a secret

1. Use a unique harmless marker in a disposable input fixture with no live login.
2. Exercise the same helper, input API, logger and recorder configuration.
3. Inspect owned stdout/stderr, action history, replay files, screenshots,
   diagnostic bundles and persisted tool state for that marker.
4. If it is retained, fix or disable the recording path, or require manual entry.
5. Repeat the relevant check after changing the runner or its recording options.

Absence of a marker in inspected artifacts is bounded evidence, not proof about
all host telemetry. A canary that failed before typing provides no evidence of
redaction. Do not run a live password through a tool just to discover what it logs.

## Recovery policy

A sign-in timeout is not a request to create another persona. Inspect current
app/account state first. A purchase timeout must also inspect transaction and
server state before another attempt. Close only the helper's session and any
daemon it owns; do not use global process kills to recover a cold runner.

# LUXLOCK for Apple Silicon Mac

[Download LUXLOCK 0.7](https://raw.githubusercontent.com/10tenni/luxware-mac/main/luxlock/releases/LUXLOCK-0.7.zip)

Requires macOS 13 or later and Screen Recording / Accessibility permission.
Quit any older copy, unzip the download, move LUXLOCK.app to a writable Applications folder, and reopen.
The app is Developer ID signed, not Apple-notarized. Secure timestamping was unavailable in the build environment.

## Version 0.7: permission retention

- The app and update helper use a persistent Developer ID signing identity. Earlier ad hoc signatures were tied to each exact build.
- Permission checks request only missing access. If both permissions are granted, the Permissions button leaves them alone.
- The release build script refuses an ad hoc fallback.
- The rejected icon is not included.

**One more approval may be needed when upgrading from 0.6 or earlier.** After approving this new identity, future builds signed with the same identity should retain permissions. macOS controls consent and can still request it again after system changes or revocation. No automatic permission grants or system privacy database edits are used.

The changed-build test confirmed that a later build keeps, and satisfies, the same designated code identity requirement. Actual TCC approvals were not modified during testing.

## Retained response improvements

- Stronger default response: strength 0.68, correction cap 80, deadzone 0.5.
- Fast response preset: strength 0.78, correction cap 100, deadzone 0.35.
- Existing older settings upgrade once while retaining the activation key and display. You can lower strength and save it afterward.
- Nametag sampling uses fewer vertical samples and more horizontal detail. Synthetic tracking-only median was 0.506 ms per frame versus 0.628 ms previously, approximately 19% less CPU tracking time. This is not a measured improvement in Roblox latency.
- Red text-shaped nametag gating, short bounded motion prediction, and immediate correction stops on tag loss are retained.

Aim below a visible **red-lettered nametag** and hold your configured activation key. Release to stop or select another target. White lettering on a red bar is not supported. Small, covered, blurred, or unusually styled names may be rejected. Similar text and UI can still cause false matches. The tracker estimates a body point beneath the name; it does not read player identities or game memory.

If input overshoots, reduce Strength. Relative input is experimental; use the bounded cursor mode if Roblox ignores it.

## Automatic updates

LUXLOCK 0.4 and later include this signed feed:

https://raw.githubusercontent.com/10tenni/luxware-mac/main/luxlock/latest.json

Use **Updates → Check now**. A verified newer release downloads and can install when you quit, with the old app retained as a backup. Automatic checks run on launch and every six hours when enabled. The app must be in a location your account can write to.

Release metadata is signed with the publisher's private key; installed apps contain only the public verification key. Downloads are checked by size, SHA-256, archive validation, bundle identity, build number, and macOS code signature. Never distribute the publisher's private signing key.

## Verification and limitations

Local build, synthetic tracking tests, rendered-text acquisition, motion prediction, and signed-package checks passed. This release has not been tested in live Roblox gameplay. No guaranteed accuracy or game-developer approval is claimed.

Screen frames remain local. No audio capture, telemetry, credentials, memory access, or injection is used. Update requests go to GitHub; GitHub may log ordinary connection data such as IP addresses.

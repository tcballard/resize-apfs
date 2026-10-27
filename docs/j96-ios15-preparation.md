# J96 iOS 15 preparation — unvalidated device build

Base: ac1658923378dcb800523d7dcd45002fc2bc5862.
Branch: j96/ios15-readonly-prep.
Target: iPad5,1 / J96AP, last verified iOS 15.8.3.
The owner states the iPad was wiped and contains no user data to back up.
The owner explicitly authorizes pursuing APFS resizing and internal installation.
No device operation or storage mutation was performed by this preparation.

Changes: app/framework/helper deployment targets lowered to iOS 15; navigation
uses NavigationView; automatic scroll keyboard dismissal is guarded on iOS 16;
root navigation-bar hiding uses the older API; large progress-control sizing
removed. Storage mutation implementation and private APFS ABI are unchanged.
This is source preparation, not proof that the app compiles or the APIs work.

Validation: shell syntax, git diff whitespace, 41 Python release tests pass.
Swift compilation, Swift unit tests, Apple signing, payload packaging, native
iOS execution and APFS API compatibility remain unverified. The XPS has neither
Swift nor Xcode; local gh authentication is invalid. Upstream provides a macOS
GitHub Actions build, which can be adapted in an owner-controlled fork.

First device payload must be inspection-only (build-overlay.py without
--enable-writes), retaining the existing helper writes-disabled default.
First establish app/helper operation and validate read-only GPT/APFS inspection.
Do not remove ABI, metadata or minimum-size checks to make the device pass.
An empty/wiped user installation does not make its system GPT/APFS disposable.

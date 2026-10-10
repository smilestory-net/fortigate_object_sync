# FortiGate Object Sync

> A high-performance desktop tool and synchronization engine to compare, reconcile, and synchronize **Firewall Address and Service Objects** across multiple FortiGate configuration files and multi-VDOM environments, generating production-ready **FortiOS CLI synchronization scripts**.

<img width="1582" height="1028" alt="image" src="https://github.com/user-attachments/assets/c4a9dcad-5ce4-4360-ba45-32cd2b52cf58" />

<img width="1582" height="1009" alt="image" src="https://github.com/user-attachments/assets/7562ed54-fb36-4b2c-b50f-1065c9dfa556" />

<img width="1582" height="1009" alt="image" src="https://github.com/user-attachments/assets/7f51e83f-550a-42ec-9723-0367cf5d508c" />

---

## 📌 Key Features

* **Full Multi-File & Multi-VDOM Support**
  * Automatically detects single-VDOM (`root`) and multi-VDOM (`config vdom`) configurations.
  * Cross-analyzes objects across different config files and VDOMs, immediately pinpointing conflicting definitions (IP subnets, FQDNs, comments, group members, etc.).

* **Intuitive Decision Workflows**
  * **Single Objects**: Select a source VDOM to adopt its definition; the engine generates `set`/`unset` commands to update all other target VDOMs.
  * **Group Objects**: Choose **[Merge (Union)]** to combine all member tokens across all VDOMs, or **[Overwrite with Selected VDOM]** to enforce one VDOM's member list.
  * **Recursive Group Closure**: Automatically detects nested group members and ensures every leaf object referenced by a group exists in target VDOMs, ordered safely from leaf objects to parent groups.

* **4-Stage Precise Diff Visualizer**
  * **Unchanged**: Matching attributes are displayed in clean standard text.
  * **Modified**: Values that differ are highlighted in yellow with hover tooltips indicating target values.
  * **Deleted**: Attributes removed from the baseline definition are styled with strikethrough and marked `(deleted)`.
  * **Added**: Newly added attributes are highlighted in green with a `+ (added)` indicator.
  * **Isolated Unselected State**: Before a decision is made, `update` and `unchanged` tags are cleanly hidden, allowing unbiased side-by-side comparison of original configurations.

* **High-Speed Search & ESC Shortcut Support**
  * **Standard Search (Unquoted)**: Exact substring matching as typed (e.g., `web server`).
  * **Multi-Word Search (Enclosed in `' '`)**: Wrap keywords in single quotes (e.g., `'web server'`) to find objects containing all keywords in any order (order-independent AND logic) with simultaneous highlighting.
  * **ESC Shortcut**:
    * **Single Press**: Immediately clears the search bar input. The selected object and its current visual position on screen remain preserved.
    * **Rapid Double Press (< 450ms)**: Clears both the search bar input and all active Kind / Type dropdown filters. The selected object and its visual position remain preserved.

* **CLI Search & Navigation**
  * Real-time search with match counter (`1 / N`), prev/next arrow buttons (`▲`/`▼`), and `Enter` / `Shift+Enter` sequential navigation with active match highlighting.

* **Adaptive UI Scaling**
  * Flexible scaling presets (80% to 125%) and custom percentage input.

---

## 💻 System Requirements

| Item | Recommended Specification |
|---|---|
| **Operating System** | **Windows 10 / Windows 11 (64-bit)** |
| **Prerequisites** | **No runtime or library installation required** (Portable standalone executable provided) |
| **Display** | 1280×860 or higher (High-DPI scaling fully supported) |

> 💡 **Notice**: This application is distributed as a self-contained **Windows standalone executable (`.exe`)** requiring no Python installation or setup.

---

## 🚀 How to Run

1. Extract the downloaded `fortigate_duplicate_diff_v1.0.zip` archive.
2. Double-click **`fortigate_duplicate_diff.exe`** inside the folder to launch the program.
3. Click **[Select Files...]** and choose one or more FortiGate backup files (`.conf` or `.txt`) to analyze.
4. Specify an output folder if needed (defaults to the first configuration file's directory).
5. Click **[ANALYZE]** to begin comparison.

---

## 📖 User Guide

1. **Select Configuration Files and Output Folder**
   * **Config Files**: Choose one or more FortiGate `.conf` or `.txt` configuration backups.
   * **Output Directory**: Choose a destination folder for generated CLI scripts and HTML reports (defaults to the first config file's folder).
   * Options: Check whether to automatically open the result folder upon completion, and whether to export HTML diff reports.

2. **Run Analysis**
   * Click the **`ANALYZE`** button.
   * The tool scans all files and VDOMs, listing all conflicting and missing objects.

3. **Make Synchronization Decisions**
   * Filter objects using the search bar, kind dropdown (`conflict` / `missing`), or type filter.
   * **Single Objects**: Click the radio button of the source VDOM that has the desired definition.
   * **Group Objects**: Select **`[Merge (Union)]`** or **`[Overwrite with selected VDOM]`** and pick the source VDOM.
   * **Search & ESC Shortcuts**:
     * Quickly filter object names using the search bar.
     * **Press `ESC` once**: Clears the search input (retains selection and on-screen position).
     * **Press `ESC` twice quickly**: Resets all filters (retains selection and on-screen position).

4. **Generate CLI**
   * Once all conflicts have decisions, click **`GENERATE CLI`**.
   * Output files (`report_diff_command_<conf_name>.txt`) are created in your destination folder.
   * Inspect generated FortiOS commands in the **`CLI PREVIEW`** tab or open the result folder directly.

---

## 🛡️ Safety & Reliability

* Generated CLI scripts exclusively perform safe object creations (`edit` / `set`) and explicit property unsets (`unset`).
* No unrelated firewall policies, interfaces, or system configurations are touched or deleted.
* Always review generated commands in the `CLI PREVIEW` tab before executing them in production environments.

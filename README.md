# FortiGate Object Sync

> A high-performance desktop tool and synchronization engine to compare, reconcile, and synchronize **Address and Service Objects** across multiple FortiGate configuration files and multi-VDOM environments, generating production-ready **FortiOS CLI synchronization scripts**.

<img width="1582" height="1028" alt="image" src="https://github.com/user-attachments/assets/c4a9dcad-5ce4-4360-ba45-32cd2b52cf58" />

<img width="1582" height="1009" alt="image" src="https://github.com/user-attachments/assets/7562ed54-fb36-4b2c-b50f-1065c9dfa556" />

<img width="1582" height="1009" alt="image" src="https://github.com/user-attachments/assets/7f51e83f-550a-42ec-9723-0367cf5d508c" />

---

## 📌 Key Features

* **Full Multi-File & Multi-VDOM Support**
  * Automatically detects single-VDOM (`root`) and multi-VDOM (`config vdom`) configurations.
  * Cross-analyzes objects across different config files and VDOMs, immediately pinpointing conflicting definitions (IP subnets, FQDNs, comments, group members, etc.).

* **Intuitive Compare / Select Workflows**
  * **Single Objects**: Select a source VDOM to adopt its definition; the engine generates `set`/`unset` commands to update all other target VDOMs.
  * **Group Objects**: Choose **[Merge (Union)]** to combine all member tokens across all VDOMs, or **[Overwrite with Selected VDOM]** to enforce one VDOM's member list.
  * **Custom Group Member Editing (+)**: In 'Overwrite with Selected VDOM' mode for group objects, clicking the `+` [Edit Members] button on the baseline VDOM card displays the full pool of members combined across all VDOMs (Merge union). Users can freely add or remove members via checkboxes with instant search filtering.
  * **Recursive Group Closure**: Automatically detects nested group members and ensures every leaf object referenced by a group exists in target VDOMs, ordered safely from leaf objects to parent groups.

* **Identical Definition Consolidation (IDENTICAL DEF)**
  * **100% Identical Attribute Detection**: Automatically discovers duplicate objects that share identical functional parameters (IP/subnet, FQDN, port ranges, group members) but have different names (e.g., `HTTP` vs `WEB`, `HTTP_SRV` vs `WEB_SRV`).
  * **Automatic Exclusion of Default Objects**: Standard FortiOS built-in system objects (`all`, `FTP_GET`, `FTP_PUT`, `EMS_ALL_UNKNOWN_CLIENTS`, `FCTEMS_ALL_FORTICLOUD_SERVERS`, etc.) are automatically excluded from duplicate clusters and comparison reports to eliminate noise.
  * **Universal Cross-Table Reference Crawler**: Scans across all FortiOS configuration tables including firewall policies, proxy policies, Central NAT (`central-snat-map`), VIP/DNAT (`firewall vip`), local-in policies, DoS/interface ACLs, IPsec VPN Phase 2 selectors, SSL-VPN split-tunneling portals, Policy-Based Routing (PBR `router policy`), static routes, and address groups.
  * **Safe Opt-in Workflow**: Defaults to **[Keep Existing (Do Not Unify)]** with zero CLI impact. When an administrator selects a standard target name, the engine replaces all references in-place across the entire configuration before cleanly deleting (`delete`) the deprecated duplicate object.
  * **Single-VDOM Cleanup**: Supports finding and consolidating identical objects within a single firewall/VDOM configuration to clean up legacy duplication.
  * **3 Dedicated HTML Reports**: Automatically generates up to 3 interactive HTML reports (`report_diff_property.html`, `report_diff_property_sync_ref.html`, `report_fgt_diff_identical_def.html`).

* **Session Save & Resume (State Persistence)**
  * When handling hundreds or thousands of conflicting objects that cannot be completed in one sitting, click **`[SAVE SESSION]`** at any point to save your entire progress to a portable `.fgtsync` session file.
  * Resuming later or on another machine is as simple as opening the `.fgtsync` file directly from **`[Select Files...]`**: all original configuration snapshots and your selected baselines are 100% restored immediately without needing the original `.conf` files.

* **4-Stage Precise Diff Visualizer**
  * **Unchanged**: Matching attributes are displayed in clean standard text.
  * **Modified**: Values that differ are highlighted in yellow with hover tooltips indicating target values.
  * **Deleted**: Attributes and group members removed from the baseline definition are styled with strikethrough and a `-` prefix (`-attribute` / `-member`).
  * **Added**: Newly added attributes and group members are styled with a `+` prefix (`+attribute` / `+member`).
  * **Isolated Unselected State**: Before a decision is made, update and unchanged tags are cleanly hidden, allowing unbiased side-by-side comparison of original configurations.

* **High-Speed Search & ESC Shortcut Support**
  * **Standard Search (Unquoted)**: Exact substring matching as typed (e.g., `web server`).
  * **Multi-Word Search (Enclosed in `' '`)**: Wrap keywords in single quotes (e.g., `'web server'`) to find objects containing all keywords in any order (order-independent AND logic) with simultaneous highlighting.
  * **ESC Shortcut**:
    * **Single Press**: Immediately clears the search bar input. The selected object and its current visual position on screen remain preserved.
    * **Rapid Double Press (< 450ms)**: Clears both the search bar input and all active Kind / Type dropdown filters. The selected object and its visual position remain preserved.

* **CLI Preview & Search Navigation**
  * Real-time search with match counter (`1 / N`), prev/next arrow buttons (`▲`/`▼`), and `Enter` / `Shift+Enter` sequential navigation with active match highlighting.
  * One-click clipboard copy for full FortiOS CLI scripts.

* **Dark Mode & Light Mode Support**
  * Full support for Light themes (System/Soft Light) and Dark themes (Antigravity Dark/Cyber Dark) to suit user preferences.

* **Adaptive UI Scaling**
  * Flexible scaling presets (80% to 125%) and custom percentage input.
  * Clean, unified button widths across all action controls.

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

1. Extract the downloaded `fortigate_duplicate_diff_v1.5.zip` archive.
2. Double-click **`fortigate_duplicate_diff.exe`** inside the folder to launch the program.
3. **Start New Analysis**:
   * Click **[Select Files...]** and choose one or more FortiGate backup files (`.conf` or `.txt`) to analyze.
   * Specify a **Save Directory** if needed (defaults to the first configuration file's directory).
   * Click **[ANALYZE]** to begin comparison.
4. **Resume Saved Session**:
   * Select a `.fgtsync` session file directly in **[Select Files...]**.
   * All object snapshots and your prior selections are immediately restored without needing the original config files.

---

## 📖 User Guide

### 1. Configuration Analysis or Session Loading
* **New Analysis**:
  * **Config Files**: Select one or more FortiGate `.conf` or `.txt` configuration backups via **[Select Files...]**.
    * Click the **`[ Collapse/Expand (▼/▶) ]`** chevron button to fold the card down to a single row (displaying compact file count and save path summary) to maximize vertical workspace.
  * **Save Directory**: Choose a destination folder for generated CLI scripts and reports (defaults to the first config file's folder).
  * **Options**: Toggle `Auto-open save folder` and `Save reports`.
  * Click **`[ANALYZE]`** to scan VDOM structures and firewall objects across all files. Upon completion, the **`[ANALYZE]`** button automatically disables to prevent redundant runs, remaining disabled until new configuration file(s) are chosen via **`[Select Files...]`**.
  * **Smart Analysis Notices**:
    * If only a single file with a single VDOM is selected, a popup alerts that no multi-source comparison conditions are met.
    * If multiple files are analyzed but no duplicate objects exist or all duplicate objects have identical attributes, an informational popup notifies that no reconciliation is necessary.
* **Load Existing Session**:
  * Select a `.fgtsync` file from **`[Select Files...]`** to restore previous progress instantly.

### 2. 'Property Sync' Tab (PROPERTY SYNC)
* **Explore & Filter Objects**:
  * Select an object tagged with orange `[Different Attributes]` or red `[Not Selected]` from the left panel.
  * **Dropdown Filters**: Filter by Kind (All / Conflict / Missing) or Type (All / Address / Addrgrp / Service / Service Group).
  * **Search & ESC Shortcuts**:
    * Type in the search box for exact substring match, or wrap terms in quotes (`'word1 word2'`) for multi-word AND search.
    * **Press `ESC` once**: Clears the search input while keeping the current selection and scroll position.
    * **Press `ESC` twice quickly**: Resets all search and filter dropdowns while maintaining selection and scroll position.
* **Resolve Conflicting Objects & Reset Selection**:
  * **Single Objects (Address / Service)**: Review attribute diffs on the right panel and click the radio button of the desired baseline VDOM.
  * **Group Objects (Addrgrp / Service Group)**:
    * **`[Merge (Union)]`**: Combines member tokens across all VDOMs into a unified group definition.
    * **`[Overwrite with Selected VDOM]`**: Select a source VDOM to enforce its exact member list across all target VDOMs.
    * **Custom Member Editor (`+` button)**: Clicking the `+` button in the top-right corner of the baseline card opens a modal displaying all members aggregated across every VDOM for this group. Features instant keyword search, select/deselect all, and reset to baseline. Selected members are directly reflected in visual diffs, session files (`.fgtsync`), and generated CLI commands.
  * **Reset Selection (🔄)**: Permanently located in the upper-right corner of the diff panel, remaining safely in a disabled state for non-conflict objects or prior to making a choice. Once a baseline selection (radio button, Merge, or Overwrite) is made, clicking the enabled **`[Reset Selection (🔄)]`** button clears the decision and immediately restores the object to the unselected (`[Not Selected]`) state.
* **Save Progress**:
  * Click **`[SAVE SESSION]`** at any time to save all decisions and current state to a portable `.fgtsync` file.

### 3. 'Name Sync' Tab (NAME SYNC)
* **Explore & Filter Clusters**:
  * Clusters of objects with identical attributes appear as cards on the left panel (e.g., `HTTP_SRV`, `WEB_SRV`).
  * Built-in FortiOS default objects (`all`, `FTP_GET`, `FTP_PUT`, `EMS_ALL_UNKNOWN_CLIENTS`, `FCTEMS_ALL_FORTICLOUD_SERVERS`, etc.) are automatically excluded from clustering to focus strictly on user-created objects.
  * Filter by type using the dropdown or search in real time for object names, IP addresses, or port numbers.
* **Select Standard Target Name (Opt-in Workflow)**:
  * Select a standard object name via the radio buttons in the top-right card (e.g., `Unify into "HTTP_SRV"`).
  * Immediately, references across policies, VIPs, NAT, VPNs, routing, and groups pointing to duplicate names (`WEB_SRV`) are updated to the chosen standard name, and commands to safely delete (`delete`) the deprecated object are scheduled in the CLI.
  * Leaving the default **[Keep Existing]** selection produces zero CLI changes and preserves all objects as-is.
* **Inspect Reference Breakdown**:
  * The bottom section displays a comprehensive breakdown table detailing everywhere each object is currently referenced (Location/Policy and Field).

### 4. 'CLI Preview' Tab (CLI PREVIEW)
* Switch between tabs corresponding to each firewall file to inspect the generated FortiOS CLI commands.
* Consolidated CLI blocks are cleanly appended at the end of each VDOM block in strict dependency order (Groups ➔ VIP ➔ VPN ➔ Routing/PBR ➔ Policies/NAT/ACL ➔ Object Deletions).
* **Search & Navigate**: Enter keywords to locate commands, navigating with `▲` / `▼` or `Enter` / `Shift+Enter`.
* **Copy All**: Click the `Copy` button to copy the entire script to clipboard.

### 5. 'Property Diff', 'Property Sync Ref', and 'Name Diff' Tabs (HTML Reports)
* **PROPERTY DIFF**: Interactive side-by-side comparison report displaying attribute discrepancies across all VDOMs.
* **PROPERTY SYNC REF**: Group reference objects report identifying dependent objects that need to be created (`Object creation required`).
* **NAME DIFF**: Identical definition report clustering objects that have duplicate configurations under different names.
* **Open in Browser**: After running analysis, click `[Open in browser]` on any report tab to view the report full-screen in your default web browser.

### 6. Generate CLI Scripts & 'Console' Tab
* Once decisions are made, click **`[GENERATE CLI]`**.
* Output CLI scripts (`report_diff_command_<conf_name>.txt`) and up to 3 HTML reports (Property Diff report, Property Sync Ref report, and Name Diff report) are created in the save directory.
* Check the **`CONSOLE`** tab for real-time progress, parsing details, and execution logs.
* Click **`[Open Save Folder]`** to open the destination folder directly in Windows Explorer.

---

## 🛡️ Safety & Reliability

* Generated CLI scripts exclusively perform safe object creations (`edit` / `set`) and explicit property unsets (`unset`).
* No unrelated firewall policies, interfaces, or system configurations are touched or deleted.
* Always review generated commands in the `CLI PREVIEW` tab before executing them in production environments.

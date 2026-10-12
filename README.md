# FortiGate Object Sync

> A specialized tool to compare and analyze **Address and Service objects** across multiple FortiGate firewall configuration files (`.conf`) or multi-vDOM environments, easily unify conflicting attributes, and automatically generate **standard FortiOS synchronization CLI commands**.

<img width="1582" height="1028" alt="image" src="https://github.com/user-attachments/assets/9dde6e6b-7408-4a89-8cf0-e4c93eb6d782" />

<img width="1582" height="1009" alt="image" src="https://github.com/user-attachments/assets/7562ed54-fb36-4b2c-b50f-1065c9dfa556" />

<img width="1582" height="1009" alt="image" src="https://github.com/user-attachments/assets/7f51e83f-550a-42ec-9723-0367cf5d508c" />

---

## 📌 Key Features

* **Full Support for Multi-File & Multi-vDOM**
  * Automatically detects and parses single-vDOM (`root`) and multi-vDOM (`config vdom`) structures.
  * Instantly identifies conflicts when objects with the same name across multiple configuration files have differing attributes (IP, subnet, FQDN, comment, members, etc.).

* **Intuitive Property Sync Workflow**
  * **Single Objects**: Select a baseline vDOM, and the tool generates CLI commands (`set`/`unset`) to apply that definition to all other target vDOMs.
  * **Group Objects**: Supports **[Merge (Union)]** to combine all member tokens across all vDOMs, or **[Overwrite with Selected vDOM]** to enforce one vDOM's member list.
  * **Custom Group Member Editing (+)**: In 'Overwrite with Selected vDOM' mode for group objects, clicking the `+` [Edit Members] button on the baseline vDOM card displays the full pool of members combined across all vDOMs (Merge union). Users can freely add or remove members via checkboxes with instant search filtering.
  * **Recursive Group Dependency Resolution (Closure)**: Automatically ensures child member objects within a group exist in target vDOMs, guaranteeing a safe execution order from **child objects creation ➔ parent group creation**.

* **Name Sync (Identical Definition Consolidation)**
  * **100% Identical Attribute Detection**: Automatically discovers duplicate objects that share identical functional parameters (IP/subnet, FQDN, port ranges, group members) but have different names (e.g., `HTTP` vs `WEB`, `WAS_SRV` vs `WEB_APP`).
  * **Universal Cross-Table Reference Crawler**: Scans across all FortiOS configuration tables including firewall policies (`firewall policy`, `proxy-policy`), Central NAT (`central-snat-map`), VIP/DNAT (`firewall vip`), local-in policies (`local-in-policy`), DoS policies and interface ACLs, IPsec VPN (Phase 2 selectors), SSL-VPN (split-tunneling portals), Policy-Based Routing (PBR `router policy`), static routes, and address groups.
  * **Safe Opt-in Workflow**: Defaults to **[Keep Existing (Do Not Unify)]** with zero CLI impact. When an administrator selects a standard target name, the engine replaces all references in-place across the entire configuration before cleanly deleting (`delete`) the deprecated duplicate object.
  * **Single-vDOM Cleanup**: Supports finding and consolidating identical objects within a single firewall/vDOM configuration to clean up legacy duplication.
  * **3 Dedicated HTML Reports**: Automatically generates up to 3 interactive HTML reports (`report_fgt_diff_identical_def.html`, etc.) to provide comprehensive visibility into object clusters and reference locations.

* **Session Save & Resume (State Persistence)**
  * When handling hundreds or thousands of conflicting objects that cannot be completed in one sitting, click **`[SAVE SESSION]`** at any point to save your entire progress to a portable `.fgtsync` session file.
  * Resuming later or on another machine is as simple as opening the `.fgtsync` file directly from **`[Select Files...]`**: all original configuration snapshots and your selected baselines are 100% restored immediately without needing the original `.conf` files.

* **Precise 4-Stage Diff Visualization**
  * **Keep (Identical)**: Attributes identical to baseline are displayed in regular text.
  * **Modify (Changed)**: Differing attributes are highlighted in yellow (hovering displays a tooltip with the target value).
  * **Delete (Removed)**: Attributes or members removed from baseline definition are displayed in red with a `-` prefix (`-Property` / `-Member`).
  * **Add (New)**: Newly added attributes or members are displayed in green with a `+` prefix (`+Property` / `+Member`).
  * **Unselected State Isolation**: Before a baseline is selected, modification/no-change tags are hidden to prevent unnecessary confusion and allow comparing raw attributes cleanly.

* **High-Speed Condition Filtering & ESC Shortcut Support**
  * **Standard Search (No quotes)**: Performs exact substring matching (e.g., searching `system web` finds objects containing that exact phrase).
  * **Multi-Word Search (Single quotes `' '`)**: Enclosing search terms in single quotes (e.g., `'system web'`) searches with an AND condition regardless of word order (`[WAS]web-system-1`, `system_web`, `web_test_system`, etc.) and simultaneously highlights all matched words.
  * **ESC Shortcut Support**:
    * **Single Press**: Instantly clears the search input field. The currently selected object and its visual scroll position (top, middle, etc.) are strictly preserved.
    * **Double Press (within 450ms)**: Clears both the search input and all dropdown filters (`Kind`, `Type`). The selection and visual scroll position are strictly preserved.

* **CLI Preview Search & Navigation**
  * Same search syntax supported directly within the generated CLI preview.
  * Match counter (`1 / N`), previous/next navigation buttons (`▲`/`▼`), and `Enter` / `Shift+Enter` sequential navigation.

* **Dark & Light Mode Support**
  * Supports light and dark themes to seamlessly adapt to user preferences.

* **Resolution-Adaptive UI Scaling**
  * Scaling presets (80% ~ 125%) as well as custom direct percentage input.
  * Uniform width layout for all top-level action buttons.

---

## 💻 System Requirements

| Item | Recommended Specification |
|---|---|
| **OS** | **Windows 10 / Windows 11 (64-bit)** |
| **Environment** | **No additional runtime or libraries required** (Standalone portable package) |
| **Display** | 1280×860 or higher (High-DPI scaling supported) |

> 💡 **Note**: This application is provided as a standalone executable (`.exe`) for Windows with no Python or third-party dependency installation required.

---

## 🚀 How to Run

1. Extract the downloaded `fortigate_duplicate_diff_v1.6.zip` file.
2. Double-click **`fortigate_duplicate_diff.exe`** in the folder to launch.
3. **Start New Analysis**:
   * Click **[Select Files...]** to select one or more FortiGate backup configuration files (`.conf` or `.txt`).
   * Specify a **Save Folder** path if needed (default: directory of the first selected file).
   * Click **[ANALYZE]** to begin analysis.
4. **Resume Previous Session**:
   * Click **[Select Files...]** and select a previously saved `.fgtsync` session file.
   * Your previous analysis data, selections, and group settings will be 100% restored immediately without needing the original `.conf` files.

---

## 📖 Detailed User Guide

### 1. Configuration Analysis & Session Loading
* **New Analysis**:
  * **Config Files**: Select FortiGate `.conf` or `.txt` files to analyze (`[Select Files...]`).
    * Use the **`[ Collapse/Expand (▼/▶) ]`** button on the right to collapse the config panel to 1 line (displaying file count and output path summary) or expand it to maximize workspace area.
  * **Save Folder**: Specify where CLI commands and reports will be saved (default: folder of the first file).
  * **Options**: Check `Auto-open Result Folder` and `Save Reports` as desired.
  * **Click [ANALYZE]**: Rapidly scans vDOM structures and firewall objects to identify conflicts and missing items. Once finished, the **`[ANALYZE]`** button is automatically disabled to prevent redundant re-runs until new files are selected via **`[Select Files...]`**.
  * **Smart Analysis Notices**:
    * If comparison conditions are not met (such as a single file with a single vDOM), an informational modal is displayed.
    * If all duplicate-named objects have 100% identical attributes and no differences or missing objects exist, an informational modal informs you immediately.
* **Resume Session**:
  * Selecting a `.fgtsync` file from **`[Select Files...]`** restores all object snapshots, selected radio buttons, and custom group edit modes immediately without requiring original config files.

### 2. 'Property Sync' Tab Guide
* **Explore & Filter Object List**:
  * Click an object in the left panel marked with an orange `[CONFLICT]` or red `[UNSELECTED]` tag.
  * **Dropdown Filters**: Filter by kind (All / Conflict / Missing) and type (All / Address / Addrgrp / Service / Svcgrp).
  * **Search**:
    * Standard Search: Exact substring match.
    * Multi-Word Search: Enclose keywords in single quotes (`'word1 word2'`) to match all words regardless of order.
  * **ESC Shortcut**:
    * **`ESC` once**: Instantly clears search input (preserving selection and scroll position).
    * **`ESC` twice rapidly (within 450ms)**: Clears search input and all dropdown filters (preserving selection and scroll position).
* **Select Baseline & Reset**:
  * **Single Objects (Address / Service)**: Inspect attribute differences across vDOMs on the right panel, then select the radio button for the baseline vDOM.
  * **Group Objects (Addrgrp / Service Group)**:
    * `[Merge (Union)]`: Synchronizes a unified group containing all members combined across all vDOMs.
    * `[Overwrite with Selected vDOM]`: Enforces the selected vDOM's member list across all target vDOMs.
    * **Custom Member Editing (`+` button)**: Clicking the `+` button opens the Member Pool modal combining all members across all vDOMs, with real-time search, select all/none, and reset. Custom edits are fully preserved in `.fgtsync` sessions and CLI output.
  * **Reset Selection (🔄)**: Located at top right of the card. Disabled until a selection is made. Clicking **`[Reset (🔄)]`** clears the selection back to initial unselected state.
* **Save Progress**:
  * Click **`[SAVE SESSION]`** at any time to save all decisions and current state to a portable `.fgtsync` file.

### 3. 'Name Sync' Tab Guide (NAME SYNC)
* **Explore & Filter Clusters**:
  * Clusters of objects with 100% identical attributes appear as cards on the left panel (e.g., `HTTP_SRV`, `WEB_SRV`).
  * Built-in FortiOS default objects (`all`, `FTP_GET`, `FTP_PUT`, `EMS_ALL_UNKNOWN_CLIENTS`, `FCTEMS_ALL_FORTICLOUD_SERVERS`, etc.) are automatically excluded from clustering to focus strictly on user-created objects.
  * Filter by type using the dropdown or search in real time for object names, IP addresses, or port numbers.
* **Select Standard Target Name (Opt-in Workflow)**:
  * Select a standard object name via the radio buttons in the top-right card (e.g., `Unify into "HTTP_SRV"`).
  * Immediately, references across policies, VIPs, NAT, VPNs, routing, and groups pointing to duplicate names (`WEB_SRV`) are updated to the chosen standard name, and commands to safely delete (`delete`) the deprecated object are scheduled in the CLI.
  * Leaving the default **[Keep Existing]** selection produces zero CLI changes and preserves all objects as-is.
* **Inspect Reference Breakdown**:
  * The bottom section displays a comprehensive breakdown table detailing everywhere each object is currently referenced (Location/Policy and Field).

### 4. 'CLI Preview' Tab Guide
* Click the file tabs at the top to inspect real-time FortiOS CLI commands for each firewall unit.
* Name consolidation decisions are automatically included in safe dependency order (Groups ➔ VIPs ➔ VPNs ➔ Routing ➔ Policy/NAT ➔ Delete deprecated objects).
* **Search & Navigate**: Type keywords in the search bar and navigate matches using `▲`/`▼` or `Enter` / `Shift+Enter`.
* **Copy All**: Click the `COPY` button at the top right to copy the entire script to clipboard.

### 5. 'Property Diff', 'Property Sync Ref', 'Name Diff' Tabs (HTML Reports)
* **Property Diff (PROPERTY DIFF)**: View an interactive HTML report comparing object attribute differences across vDOMs directly in the GUI.
* **Property Sync Ref (PROPERTY SYNC REF)**: Review objects requiring creation in target vDOMs due to cross-references (`Object creation required`).
* **Name Diff (NAME DIFF)**: View an interactive report analyzing clusters of identical objects and reference locations.
* **Open in Browser**: Click `[Open in Browser]` on any report tab to view in full screen in your default browser.

### 6. Generate CLI & 'Console' Verification
* After completing selections in Property Sync and Name Sync, click **`[GENERATE CLI]`** at the top.
* Synchronization CLI scripts (`report_diff_command_<filename>.txt`) and up to 3 interactive HTML reports are generated in the designated save directory.
* Check the **`CONSOLE`** tab for execution completion logs and real-time output.
* Click **`[Open Result Folder]`** to immediately open the output folder in File Explorer.

---

## 🛡️ Safety & Precautions

* CLI commands generated by this tool strictly perform **firewall object creation (`edit` / `set`) and cleanup of obsolete attributes (`unset`)**.
* Firewall policies or unrelated configuration blocks are never deleted arbitrarily, ensuring safe deployment in production environments.
* Administrators should always review generated CLI commands in the `CLI Preview` tab before applying them to physical firewall equipment.

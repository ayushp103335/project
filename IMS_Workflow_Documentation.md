# AXES: IMS Execution (Regression) Workflow Documentation

This document provides a comprehensive technical overview of the IMS Execution workflow within the AXES platform, detailing the lifecycle from server monitoring to real-time reporting.

## 1. High-Level Lifecycle

The workflow is categorized into six major stages:

1.  **Server Monitoring:** Real-time tracking of remote IMS machine availability.
2.  **Synchronization:** Git updates and test discovery on remote machines.
3.  **Execution Setup:** User credential verification and dynamic environment preparation.
4.  **Triggering the Run:** Orchestration of the automation process via Maven and Scheduled Tasks.
5.  **Tracking & Reporting:** Real-time result updates via HTTP callbacks.
6.  **Review & Analysis:** Historical comparison and failure diagnostics.

---

## 2. Detailed Technical Breakdown

### Stage 1: Server Monitoring & Availability
*   **Real-time Status:** AXES monitors IMS servers (e.g., `imsautomate02`).
*   **Socket.IO Integration:** Uses WebSockets to broadcast server states (Busy/Available). When a session starts, the server is marked "Busy" to prevent conflicts.

### Stage 2: Synchronization & Discovery
*   **Git Updates:** Triggers `git pull` on the remote machine via `gitPull.ps1` to sync the latest TestNG scripts.
*   **Test Discovery:** The backend (`suiteAndTests.js`) scans Java files using advanced Regex to identify `@Test` methods, `dependsOnMethods`, and enabled/disabled states.
*   **Metadata Generation:** This data is served as a searchable tree structure for the frontend.

### Stage 3: Execution Setup (The Preparation)
This stage prepares the remote environment for a "lights-out" execution.
*   **Credential Verification:** Uses `check_credentials.ps1` to verify Windows login details before proceeding.
*   **Dynamic XML Generation:** 
    *   Builds a custom `testNg.xml` string based on user selections.
    *   Saves the file to a **shared network path** accessible by the remote server.
*   **Configuration Sync:** 
    *   Uses `copy_config_file.ps1` to move `config.properties` from the AXES server to `C:\IMSAutomation` on the remote host.

### Stage 4: Triggering the Run (The Execution)
AXES ensures a clean run by managing processes and using the Windows Task Scheduler.
*   **Process Cleanup:** Runs `taskkill` commands on the remote machine to clear existing instances of `ims.exe`, `excel.exe`, `uft.exe`, etc., via `start_execution.ps1`.
*   **Maven Orchestration:** Triggers either `mvn test` (with project update) or `mvn surefire:test` using the dynamic XML file.
*   **Scheduled Task Strategy:** 
    *   Creates a temporary Windows Scheduled Task on the remote machine.
    *   Runs the task immediately in the background, allowing the Node.js server to remain responsive.
    *   Deletes the task definition once triggered.

### Stage 5: Tracking & Reporting (The Feedback Loop)
Ensures granular data capture for every test method.
*   **Initialization:** A `Batch` entry is created, and all selected tests are inserted into the `Results` table as `PENDING`.
*   **Callback Mechanism:** The remote automation script sends an HTTP POST to the AXES `/updateTestStatus` API upon completion of each test case.
*   **Data Capture:** Updates the database with:
    *   **Status:** (PASS, FAIL, WARNING, SKIPPED).
    *   **Diagnostics:** Full Stack Trace and Exceptions for failed cases.
    *   **Timing:** Start/End timestamps and total duration.

### Stage 6: Review & Analysis
*   **Dashboard Summary:** Pass/Fail counts updated live.
*   **Regression Analysis:** Historical storage allows for comparing current runs against previous batches.

---

## 3. PowerShell Scripts Reference

| Script Name | Purpose | Location |
| :--- | :--- | :--- |
| `check_credentials.ps1` | Validates Windows login on remote machine. | `.../execution-files/IMS/` |
| `copy_config_file.ps1` | Syncs properties/configs to remote `C:\` drive. | `.../execution-files/IMS/` |
| `gitPull.ps1` | Synchronizes the automation codebase via Git. | `.../execution-files/IMS/` |
| `start_execution.ps1` | Cleans processes and triggers the Maven run. | `.../execution-files/IMS/` |
| `connect_execution_servers.ps1`| Establishes visual connection (RDP/VNC). | `.../execution-files/IMS/` |

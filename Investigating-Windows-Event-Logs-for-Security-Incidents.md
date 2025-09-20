# Investigating Windows Event Logs for Security Incidents

## Introduction

Windows Event Logs are an essential resource for detecting and investigating security incidents. In this project, I carried out an in-depth analysis of Windows Event Logs to uncover suspicious login activities and correlate them with successful authentication attempts. By utilizing built-in tools such as Event Viewer and PowerShell, along with Microsoft’s Log Parser utility, I was able to collect, filter, parse, and analyze logs for actionable forensic insights.

---

## Lab Setup

The investigation was performed in a controlled environment using a Windows virtual machine. This allowed simulation of login attempts and ensured safe experimentation.

**Environment Configuration**:

* Windows 10 Virtual Machine (VMware Workstation)
* Local Administrator privileges enabled

---

## Pre-requisites

To complete this project, I prepared with the following:

* A working knowledge of Windows operating system features
* Familiarity with command-line interface usage
* Basic understanding of Windows Event Logging and security-related Event IDs

---

## Tools Utilized

* **Event Viewer** – Native Windows utility for browsing event logs.
* **PowerShell** – Command-line interface and scripting tool for querying event data.
* **Log Parser** – Microsoft’s utility to run structured SQL-like queries against event logs.

**Log Parser Installation**:

1. Download Log Parser from the Microsoft Download Center.
2. Run the installer and complete the installation using default settings.
3. Verify installation by opening Command Prompt and typing `LogParser.exe` to check version and usage.

---

## Project Execution

### Exercise 1: Accessing Windows Event Logs using Event Viewer

**Objective:** Understand how to access and navigate Windows Event Logs using Event Viewer.

**Steps:**

1. Open the Run dialog (`Win + R`) and type `eventvwr.msc`, then press Enter.
2. Once Event Viewer is launched, expand the **Windows Logs** section.
3. Explore the different log categories:

   * Application
   * Security
   * Setup
   * System
   * Forwarded Events
4. Select **Security** under Windows Logs to review authentication-related events.
5. Scroll through events to identify login attempts, paying attention to the **Event ID** values (4624 for successful logins, 4625 for failed logins).

**Expected Outcome:** I was able to successfully navigate through the Event Viewer, access the Security logs, and observe multiple authentication events, including login attempts.

---

### Exercise 2: Filtering and Exporting Event Logs

**Objective:** Learn how to filter Security logs for specific events and export them for further analysis.

**Steps:**

1. In Event Viewer, select the **Security** log.
2. Right-click on Security and choose **Filter Current Log**.
3. In the filter window, select **Event ID** and enter `4625` (failed login attempts).
4. Click **OK** to apply the filter. The Security log now displays only failed logins.
5. Right-click on the filtered Security log and select **Save Filtered Log File As**.
6. Save the filtered logs with the name `FailedLogins.evtx`.

**Expected Outcome:** I obtained a filtered set of Security events containing only failed login attempts, exported as a `.evtx` file for deeper investigation.

---

### Exercise 3: Parsing Event Logs using Log Parser

**Objective:** Use Log Parser to extract structured data from event logs.

**Steps:**

1. Open **Command Prompt** and navigate to the Log Parser installation directory.

2. Run the following command to parse the exported event log and extract meaningful information:

   ```bash
   LogParser.exe "SELECT TimeGenerated, EventID, EventTypeName, Message INTO FailedLogins.csv FROM FailedLogins.evtx" -i:EVT -o:CSV
   ```

   * `TimeGenerated` gives the timestamp of each event.
   * `EventID` identifies the event type (e.g., 4625 for failed logins).
   * `EventTypeName` provides the event category.
   * `Message` contains details about the event.

3. Once the command executes, open the generated `FailedLogins.csv` file in Excel or a text editor to review the extracted data.

**Expected Outcome:** I generated a CSV file (`FailedLogins.csv`) containing detailed information about failed login attempts, including timestamps and event descriptions.

---

### Exercise 4: Analyzing Event Logs using PowerShell

**Objective:** Automate failed login event detection using PowerShell.

**Steps:**

1. Open **PowerShell** with administrative privileges.

2. Run the following command to list failed login attempts directly from the Security log:

   ```powershell
   Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625} | Format-Table TimeCreated, Id, Message -AutoSize
   ```

   * `LogName='Security'` specifies the Security log.
   * `Id=4625` filters only failed login attempts.
   * The output displays the event time, ID, and details.

3. To save the results for documentation, execute:

   ```powershell
   Get-WinEvent -FilterHashtable @{LogName='Security'; Id=4625} | Format-Table TimeCreated, Id, Message -AutoSize | Out-File -FilePath FailedLogins.txt
   ```

**Expected Outcome:** The PowerShell console displayed a list of failed login attempts, and the results were successfully exported to `FailedLogins.txt` for later reference.

---

### Exercise 5: Correlating Events for Comprehensive Analysis

**Objective:** Correlate failed login attempts (4625) with successful logins (4624) to identify potential intrusions.

**Steps:**

1. Open Event Viewer and locate successful login events by filtering for **Event ID 4624**.

2. Using Log Parser, correlate failed login attempts with successful logins for the same users:

   ```bash
   LogParser.exe "SELECT a.TimeGenerated AS FailedLoginTime, b.TimeGenerated AS SuccessfulLoginTime, a.Message AS FailedLoginMessage, b.Message AS SuccessfulLoginMessage INTO CorrelatedLogins.csv FROM FailedLogins.evtx a JOIN SuccessfulLogins.evtx b ON a.User=b.User WHERE a.EventID=4625 AND b.EventID=4624" -i:EVT -o:CSV
   ```

   * This query joins failed login attempts with subsequent successful logins.
   * The results include timestamps and event details for both.

3. Open `CorrelatedLogins.csv` to analyze the sequence of failed and successful login attempts.

**Expected Outcome:** I successfully correlated failed login attempts with successful logins. The analysis highlighted suspicious activity where multiple failed attempts were followed by a successful login, suggesting potential brute-force or credential-stuffing attacks.

---

## Key Findings

* Multiple failed login attempts (4625) were recorded against specific accounts.
* Several accounts showed a successful login (4624) immediately after repeated failures, indicating possible unauthorized access.
* Correlation across logs allowed identification of patterns that would be missed if logs were viewed in isolation.

---

## Conclusion

This project demonstrated a complete workflow for investigating Windows Event Logs to detect security incidents. The process included:

1. Accessing and navigating logs with Event Viewer.
2. Filtering and exporting specific events.
3. Parsing logs into structured CSV files using Log Parser.
4. Automating analysis with PowerShell.
5. Correlating multiple log types for incident detection.

Through this investigation, I gained practical experience in using Windows forensic artifacts to detect and analyze potential intrusions. This project highlights the critical role of event log analysis in digital forensics, threat hunting, and incident response.


# Extracting and Interpreting Browser Artifacts on Windows

## Introduction

Web browsers store extensive information about user activities, including browsing history, cookies, cached data, download records, and stored credentials. Analyzing these browser artifacts can provide critical evidence during forensic investigations, revealing user behavior, potential data exfiltration, or malicious activity.

In this project, I extracted and analyzed browser artifacts from popular Windows browsers using specialized forensic tools, gaining insights into user activity and potential security incidents.

---

## Lab Setup

The project was conducted in a controlled environment using a Windows virtual machine:

* Windows 10 Virtual Machine (VMware Workstation)
* Administrative privileges enabled
* Browsers installed for testing: Chrome, Firefox, Edge

---

## Pre-requisites

* Basic knowledge of Windows OS
* Familiarity with command-line interface and database analysis
* Understanding of web browser storage mechanisms and SQLite databases

---

## Tools Utilized

* **WebBrowserPassView** – Recovers stored passwords from browsers
* **BrowserHistoryViewer** – Extracts and views browser history
* **SQLite Database Browser** – For exploring SQLite-based browser databases

**Installation Steps:**

1. **WebBrowserPassView:** Download from NirSoft and extract the zip to a working directory.
2. **BrowserHistoryViewer:** Download from Foxton Software and install following the prompts.
3. **SQLite Database Browser:** Download from the official website and complete installation.

---

## Project Execution

### Exercise 1: Extracting Browser History

**Objective:** Extract and review browser history from popular web browsers.

**Steps:**

1. Open **BrowserHistoryViewer**.
2. Select the browsers to analyze (Chrome, Firefox, Edge).
3. Click **Load History** to extract browsing history from selected browsers.
4. Review the displayed history, including visited URLs, visit dates, and times.

**Outcome:** I successfully extracted and analyzed browser history, obtaining a timeline of user browsing activities across different browsers.

---

### Exercise 2: Recovering Stored Passwords

**Objective:** Retrieve passwords stored in web browsers.

**Steps:**

1. Open **WebBrowserPassView**.
2. The tool automatically detects and lists stored passwords for supported browsers.
3. Review recovered passwords, including website URLs, usernames, and passwords.

**Outcome:** I recovered stored credentials, which could be critical evidence in forensic investigations or identifying potential unauthorized access.

---

### Exercise 3: Analyzing Browser Cookies

**Objective:** Extract and analyze cookies to track user activities and potential malicious behavior.

**Steps:**

1. Locate the cookies database for the target browser (e.g., `Cookies` file in Chrome user data directory).
2. Open the cookies database using **SQLite Database Browser**.
3. Browse the cookies table to examine stored cookies, including host, name, value, creation date, and expiry date.

**Outcome:** I analyzed browser cookies to identify user activity patterns, session data, and potential tracking mechanisms, which can be critical in forensic analysis.

---

### Exercise 4: Examining Browser Cache

**Objective:** Analyze browser cache to uncover information about accessed web content and resources.

**Steps:**

1. Locate the cache directory for the target browser (e.g., `Cache` folder in Chrome user data directory).
2. Use **BrowserHistoryViewer** to load cache entries:

   * Go to `File > Load Cache` and select the cache folder.
3. Review cached items, including URLs, cache types, and sizes.

**Outcome:** I successfully examined cached web content, providing insight into visited websites and resources accessed by the user.

---

### Exercise 5: Interpreting Download Records

**Objective:** Extract and interpret browser download records.

**Steps:**

1. Locate the downloads database for the target browser (e.g., `History` file in Chrome user data directory).
2. Open the downloads database using **SQLite Database Browser**.
3. Browse the downloads table to view records, including download URLs, file paths, start times, and end times.

**Outcome:** I successfully identified files downloaded by the user, including timestamps and download locations, providing evidence of user activity and potential data transfers.

---

## Key Findings

* Extracted complete browser history for Chrome, Firefox, and Edge.
* Recovered stored credentials, providing insights into account usage.
* Analyzed cookies and cache to understand browsing patterns.
* Identified downloaded files and their associated metadata.
* Correlation of browser artifacts provided a comprehensive view of user behavior and potential security incidents.

---

## Conclusion

This project demonstrated a thorough approach to analyzing browser artifacts on Windows. By leveraging **BrowserHistoryViewer**, **WebBrowserPassView**, and **SQLite Database Browser**, I was able to:

1. Extract user browsing history and download records.
2. Recover stored credentials from browsers.
3. Analyze cookies and cache for user activity and potential malicious behavior.
4. Interpret browser artifacts to provide actionable forensic insights.

Through this project, I gained practical experience in **browser forensics**, enhancing my skills in uncovering evidence of user activity and potential security incidents on Windows systems.

# Analyzing Windows Registry for Evidence of Malicious Activity

## Introduction

The Windows Registry is a hierarchical database that stores low-level configuration settings for the operating system and installed applications. During a forensic investigation, the Registry is an invaluable source of evidence because it can reveal traces of user activity, persistence mechanisms, and malware artifacts.

In this project, I analyzed a Windows memory image using the **Volatility framework** to extract and investigate Windows Registry hives. The analysis focused on identifying user account details, persistence mechanisms, and recently accessed applications that could indicate malicious activity.

---

## Lab Setup

The analysis was performed in a controlled lab environment with the following setup:

* Windows 10 Virtual Machine (VMware Workstation)
* Memory image acquired for forensic analysis
* Administrative privileges enabled

---

## Pre-requisites

Before starting the project, the following knowledge areas were required:

* Fundamentals of Windows operating system internals
* Understanding of the Windows Registry structure and hives
* Familiarity with command-line interfaces

---

## Tools Utilized

* **Volatility** – Advanced open-source memory forensics framework

**Installation of Volatility:**

1. Download Volatility from the official website.
2. Extract the contents to a working directory.
3. Ensure Python 2.7 is installed and configured, as Volatility requires it.
4. Verify installation by running `volatility --info` in the command prompt.

---

## Project Execution

### Exercise 1: Extracting Windows Registry Hives from a Memory Image

**Objective:** Extract Windows Registry hives from the memory image using Volatility.

**Steps:**

1. Open Command Prompt and navigate to the Volatility directory.

2. Run the following command to identify supported profiles for the memory image:

   ```bash
   volatility -f <memory_image> imageinfo
   ```

3. Once the correct profile is identified, list all Registry hives with the command:

   ```bash
   volatility -f <memory_image> --profile=<profile> hivelist
   ```

   This displays the virtual addresses of key hives (e.g., SAM, SYSTEM, SOFTWARE, NTUSER.DAT).

4. Dump Registry hives to a specified directory:

   ```bash
   volatility -f <memory_image> --profile=<profile> dumpregistry -o <virtual_address> -D <output_directory>
   ```

**Expected Outcome:** I successfully extracted the Windows Registry hives (SAM, SYSTEM, SOFTWARE, NTUSER.DAT) and saved them for analysis.

---

### Exercise 2: Analyzing the SAM Hive for User Information

**Objective:** Extract user account information from the SAM hive.

**Steps:**

1. Using the SAM hive extracted in Exercise 1, run Volatility’s `hashdump` plugin:

   ```bash
   volatility -f <memory_image> --profile=<profile> hashdump -y <system_hive> -s <sam_hive>
   ```

2. This command extracts usernames and corresponding password hashes stored in the SAM hive.

**Expected Outcome:** I obtained a list of user accounts along with hashed passwords. These artifacts can be analyzed further for account usage and potential brute-force activity.

---

### Exercise 3: Investigating Autorun Entries in the Software Hive

**Objective:** Identify autorun entries that may represent persistence mechanisms for malware.

**Steps:**

1. Using the extracted SOFTWARE hive, run the following command to review autorun entries:

   ```bash
   volatility -f <memory_image> --profile=<profile> printkey -o <software_hive_virtual_address> -K "Microsoft\Windows\CurrentVersion\Run"
   ```

2. The output displays all applications set to execute automatically at system startup.

**Expected Outcome:** I identified autorun entries within the SOFTWARE hive. Suspicious or unusual entries could indicate malware attempting to maintain persistence.

---

### Exercise 4: Examining User Assist Keys in the NTUSER.DAT Hive

**Objective:** Review User Assist keys to determine recently accessed applications by a user.

**Steps:**

1. Using the extracted NTUSER.DAT hive, run Volatility’s `userassist` plugin:

   ```bash
   volatility -f <memory_image> --profile=<profile> userassist -i
   ```

2. The command lists recently executed applications along with execution counts and timestamps.

**Expected Outcome:** I obtained a timeline of programs accessed by the user, which helped in identifying unusual or potentially malicious activity.

---

### Exercise 5: Correlating Registry Artifacts for Comprehensive Analysis

**Objective:** Combine findings from multiple Registry hives to identify evidence of malicious activity.

**Steps:**

1. Reviewed user account information from the **SAM hive**.
2. Analyzed persistence mechanisms in the **SOFTWARE hive**.
3. Correlated recently accessed applications from the **NTUSER.DAT hive**.
4. Cross-checked consistency between user activity and suspicious entries.

**Expected Outcome:** By correlating data across hives, I identified possible evidence of persistence and suspicious user activity. For example, autorun entries pointing to unknown executables matched with unusual program execution patterns from the User Assist keys.

---

## Key Findings

* Extracted and reviewed all major Registry hives from the memory image.
* Discovered user account details including password hashes for potential offline cracking.
* Identified autorun entries that could indicate malware persistence.
* Observed unusual application execution history from User Assist keys.
* Correlation across Registry artifacts strengthened the evidence of suspicious activity.

---

## Conclusion

This project demonstrated a complete process of Registry forensics using **Volatility**. The investigation included:

1. Extracting Windows Registry hives from memory.
2. Analyzing user accounts and password hashes from the SAM hive.
3. Identifying autorun entries from the SOFTWARE hive.
4. Investigating application usage patterns via User Assist keys in NTUSER.DAT.
5. Correlating artifacts across multiple hives for comprehensive analysis.

Through this project, I gained hands-on experience in **memory forensics and Registry artifact analysis**, both of which are essential skills for detecting malware persistence, account compromise, and suspicious user behavior during forensic investigations.


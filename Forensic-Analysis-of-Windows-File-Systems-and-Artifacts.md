# Forensic Analysis of Windows File Systems and Artifacts

## Introduction

Windows file systems and associated artifacts contain critical information for forensic investigations. Analyzing these artifacts can reveal file activity, user behavior, and evidence of malicious actions.

In this project, I performed a comprehensive analysis of a Windows file system, created a forensic image, and examined key artifacts such as the Master File Table (MFT), Prefetch files, and Shellbags. This analysis provided insights into user and system activity, highlighting potential security incidents.

---

## Lab Setup

The project was conducted using a Windows environment with a forensic-ready setup:

* Windows 10 Virtual Machine (VMware Workstation)
* Administrative privileges enabled
* Forensic tools installed for disk imaging, file system analysis, and artifact examination

---

## Pre-requisites

* Basic understanding of Windows OS and file system structure
* Familiarity with command-line interface
* Knowledge of NTFS and key Windows artifacts

---

## Tools Utilized

* **FTK Imager** – Forensic disk imaging tool
* **Autopsy** – Digital forensics platform and graphical interface for The Sleuth Kit
* **Windows File Analyzer** – For analyzing Prefetch and other Windows artifacts

**Installation Steps:**

1. **FTK Imager:** Download from AccessData, run installer, follow on-screen instructions.
2. **Autopsy:** Download from official website, run installer, follow on-screen instructions.
3. **Windows File Analyzer:** Download from official website, run installer, follow on-screen instructions.

---

## Project Execution

### Exercise 1: Creating a Forensic Image using FTK Imager

**Objective:** Create a forensic image of a disk for analysis.

**Steps:**

1. Open FTK Imager.
2. Navigate to `File > Create Disk Image`.
3. Select the source type (e.g., Physical Drive) and choose the disk to image.
4. Follow prompts to select the image format (e.g., E01) and destination path.
5. Complete the imaging process and verify the image integrity using hash values (MD5/SHA1).

**Outcome:** I successfully created a complete forensic image of the disk, stored in E01 format, ready for analysis.

---

### Exercise 2: Analyzing File System with Autopsy

**Objective:** Explore the forensic image and examine the file system hierarchy.

**Steps:**

1. Open Autopsy and create a new case.
2. Add the forensic image created in Exercise 1 as a data source.
3. Navigate the file system hierarchy through Autopsy’s interface.
4. Examine critical directories such as:

   * `C:\Users`
   * `C:\Program Files`
   * `C:\Windows`
5. Review file properties and metadata for key system and user files.

**Outcome:** I successfully explored the file system and identified significant directories and files, providing a foundation for artifact extraction.

---

### Exercise 3: Extracting and Analyzing MFT (Master File Table)

**Objective:** Analyze the MFT to track file creation, modification, and deletion events.

**Steps:**

1. Locate the `$MFT` file within the NTFS file system in Autopsy.

2. Extract the `$MFT` file to a local working directory.

3. Use **MFTECmd** to parse the MFT:

   ```bash
   MFTECmd.exe -f <path_to_MFT> -o <output_directory>
   ```

4. Review the parsed output to identify timestamps and file activity (created, modified, deleted).

**Outcome:** I obtained a detailed record of file system activity, which included creation, modification, and deletion events, critical for forensic analysis.

---

### Exercise 4: Analyzing Windows Prefetch Files

**Objective:** Determine recently executed applications using Prefetch files.

**Steps:**

1. Open Windows File Analyzer.
2. Load Prefetch files from the forensic image (typically located in `C:\Windows\Prefetch`).
3. Review execution details, including application names and last run times.

**Outcome:** I was able to generate a list of recently executed applications with execution timestamps, which provided insight into system and user activity.

---

### Exercise 5: Investigating Recent Activity using Shellbags

**Objective:** Examine Shellbags to identify recently accessed directories and files.

**Steps:**

1. Extract NTUSER.DAT files for each user from the forensic image using Autopsy.

2. Use **ShellBags Explorer (SBECmd)** to parse and analyze the NTUSER.DAT files:

   ```bash
   SBECmd.exe -f <path_to_NTUSER.DAT> -o <output_directory>
   ```

3. Review Shellbags output to determine the directories and files accessed by each user.

**Outcome:** I identified recently accessed directories and files for each user, which provided insights into user behavior and potential security incidents.

---

## Key Findings

* Successfully created a forensic disk image and verified integrity.
* Explored file system and identified key directories and system files.
* Extracted and analyzed the MFT to reconstruct file activity timelines.
* Analyzed Prefetch files to identify recently executed applications.
* Examined Shellbags to determine user activity and recently accessed locations.

---

## Conclusion

This project provided comprehensive exposure to Windows file system forensics. Through disk imaging, file system exploration, and artifact analysis, I was able to:

1. Reconstruct file activity and access timelines.
2. Identify user behavior through Prefetch and Shellbag analysis.
3. Generate evidence to support potential security incident investigations.

The exercises enhanced my skills in **Windows digital forensics**, providing practical experience in handling, analyzing, and interpreting key artifacts for investigative purposes.

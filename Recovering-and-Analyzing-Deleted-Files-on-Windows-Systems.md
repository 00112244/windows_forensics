# Recovering and Analyzing Deleted Files on Windows Systems

## Introduction

Deleted files on Windows systems can still contain crucial information for forensic investigations. Recovering and analyzing these files can reveal evidence of user activities, unauthorized actions, or malicious behavior.

In this project, I recovered and analyzed deleted files using a combination of **Recuva**, **FTK Imager**, and **Autopsy**. The process included creating forensic images, examining deleted files, analyzing metadata, and correlating file activity with system events to understand the context of deletions.

---

## Lab Setup

The project was performed in a controlled forensic lab environment:

* Windows 10 Virtual Machine (VMware Workstation)
* Administrative privileges enabled
* Target disk for file recovery

---

## Pre-requisites

* Basic understanding of Windows OS
* Familiarity with command-line interface and file system structure
* Knowledge of NTFS and forensic analysis principles

---

## Tools Utilized

* **Recuva** – Tool to recover deleted files
* **FTK Imager** – Forensic disk imaging tool
* **Autopsy** – Digital forensics platform for file analysis

**Installation Steps:**

1. **Recuva:** Download from the official website and complete installation.
2. **FTK Imager:** Download from AccessData and install following on-screen prompts.
3. **Autopsy:** Download from the official website and complete installation.

---

## Project Execution

### Exercise 1: Recovering Deleted Files using Recuva

**Objective:** Recover deleted files from a Windows disk.

**Steps:**

1. Open **Recuva**.
2. Select the type of files to recover (e.g., All Files).
3. Choose the location or drive to scan for deleted files.
4. Start the scan and wait for completion.
5. Review the list of recoverable files and select the desired files.
6. Click **Recover** and choose a location to save the recovered files.

**Outcome:** I successfully recovered deleted files and stored them in a secure directory for analysis.

---

### Exercise 2: Creating a Forensic Image of the Disk using FTK Imager

**Objective:** Create a forensic image of the disk for detailed examination.

**Steps:**

1. Open **FTK Imager**.
2. Navigate to `File > Create Disk Image`.
3. Select the source type (e.g., Physical Drive) and choose the disk to image.
4. Follow prompts to select the image format (e.g., E01) and destination path.
5. Complete the imaging process and verify integrity using hash values (MD5/SHA1).

**Outcome:** I successfully created a forensic image of the disk, preserving the deleted files for detailed analysis.

---

### Exercise 3: Analyzing Deleted Files using Autopsy

**Objective:** Examine deleted files and their contents within a forensic image.

**Steps:**

1. Open **Autopsy** and create a new case.
2. Add the forensic image created in Exercise 2 as a data source.
3. Navigate to the **File Analysis** module.
4. Apply filters to display only deleted files.
5. Review the deleted files and examine their contents.

**Outcome:** I successfully analyzed deleted files and verified their contents, recovering critical evidence that could be relevant to forensic investigations.

---

### Exercise 4: Examining Metadata of Recovered Files

**Objective:** Extract metadata from recovered files to gain additional context.

**Steps:**

1. In **Autopsy**, locate the recovered files.
2. Right-click a file and select **Extract File Metadata**.
3. Review metadata including:

   * Creation, modification, and access times
   * File size and type
   * File ownership and permissions

**Outcome:** I obtained detailed metadata for each recovered file, providing additional context regarding file origin and activity.

---

### Exercise 5: Correlating Recovered Files with System Events

**Objective:** Understand the context of file deletion by correlating with system events.

**Steps:**

1. In **Autopsy**, examine the system timeline surrounding the deletion events.
2. Identify relevant events such as:

   * File creation, modification, and deletion
   * User logins and logouts
   * Application execution around the deletion time
3. Correlate these events with the recovered files to determine the context and potential reasons for deletion.
4. Document findings and provide recommendations for further investigation.

**Outcome:** I successfully correlated deleted files with system events, gaining insight into the user and system activity that led to the deletions. This provided a comprehensive understanding of the context and potential security implications.

---

## Key Findings

* Successfully recovered deleted files using Recuva.
* Created a forensic disk image for detailed analysis.
* Analyzed the contents and metadata of recovered files using Autopsy.
* Correlated deleted files with system events to understand the context of deletions.
* Identified potential indicators of malicious activity or unauthorized file manipulation.

---

## Conclusion

This project demonstrated the end-to-end process of recovering and analyzing deleted files on Windows systems. By combining **Recuva**, **FTK Imager**, and **Autopsy**, I was able to:

1. Recover deleted files and preserve them in a forensic image.
2. Analyze file contents and metadata to extract meaningful information.
3. Correlate deleted files with system events to understand the context and implications of file deletion.

This project strengthened my practical skills in **Windows file recovery and digital forensics**, enabling me to uncover critical evidence and reconstruct user and system activity during investigations.

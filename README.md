# NX212 - Automated Forensic Investigation Analyzer

![NX212 Cover Image](NX212.png)

> **Project:** Automated Forensics Toolkit

---

## 📖 Executive Summary

The **NX212 Analyzer** is a comprehensive Bash-based digital forensics framework designed to streamline the investigation lifecycle. It serves as a unified orchestration engine that wraps powerful industry-standard tools into a single, interactive command-line interface. 

[Image of digital forensics process flow]


By automating tool execution, dependency management, and report generation, NX212 significantly reduces the manual effort required to analyze memory dumps and disk images, allowing investigators to focus on intelligence gathering rather than tool configuration.

---

## ✨ Key Features

* **🕵️ Multi-Tool Orchestration:** Seamlessly integrates and manages execution for:
    * **Bulk Extractor:** Rapidly extracts artifacts like emails, URLs, and credit card numbers.
    * **Binwalk:** Analyzes and extracts firmware images and embedded files.
    * **Foremost:** Carves files based on headers, footers, and internal data structures.
    * **Volatility:** Performs deep memory forensics.
* **🧠 Intelligent Memory Analysis:**
    * Automates **Volatility 2.5** operations.
    * Auto-detects image profiles using `imageinfo` before running plugins to prevent errors.
    * Supports a wide range of plugins including `pslist`, `netscan`, `hivelist`, and `hashdump`.
* **📡 Network Heuristics:**
    * Automatically scans extraction outputs for `.pcap` files.
    * Provides an interactive prompt to launch **Wireshark** immediately upon detecting network artifacts.
* **🔐 Credential Hunting:**
    * Performs static analysis on raw images using `strings`.
    * Applies regex filters to hunt for high-value keywords like "password", "token", "auth", and "secret".
* **⚙️ Self-Healing Environment:**
    * Checks for required dependencies (`figlet`, `tree`, `strings`, etc.) at startup.
    * Auto-installs missing tools via `apt-get` and downloads portable Volatility binaries if needed.

---

## 🚀 Getting Started

### Prerequisites

* **Operating System:** Linux (Kali Linux or Debian-based distribution recommended).
* **Privileges:** The script requires `root` access to mount images and execute system-level tools.

### Installation

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/ibrianoz/NX212.git](https://github.com/ibrianoz/NX212.git)
    cd NX212
    ```

2.  **Make Executable:**
    ```bash
    chmod +x nx212.sh
    ```

3.  **Run with Evidence File:**
    ```bash
    sudo ./nx212.sh /path/to/memory_dump.img
    ```

---

## 🖥️ Usage Guide

### The Interactive Menu
Upon launching, the script presents a multi-selection menu allowing you to run individual tools or a full audit chain.

```text
==========================================================================
   Here is what's on the MENU
==========================================================================
[+] 1 - Use bulk_extractor
[+] 2 - Use binwalk
[+] 3 - Use foremost
[+] 4 - Use volatility & extract network traffic
[+] 5 - Extract strings & scan for credentials
[+] 6 - Use all tools (run everything)
...
Example Workflows
Quick Triage: Select Option 5 to quickly scan for plaintext credentials and strings.

Deep Dive: Select Option 6 to run all extractors and memory analysis plugins sequentially.

Network Investigation: Select Option 1 or 4. If a PCAP is found, the script will ask:

🔍 Would you like to open the network file with Wireshark? (y/n)

📂 Output Structure
All artifacts are organized into a dedicated directory based on the evidence file name, which is zipped upon completion.

Plaintext

Evidence_File_Name/
├── bulk_extractor_output/   # Scraped artifacts (emails, domains)
├── binwalk_output/          # Extracted firmware/file data
├── foremost_output/         # Carved files (jpg, pdf, doc)
├── vol_ProfileName/         # Volatility plugin outputs (txt)
├── STRINGS/                 # Raw strings and filtered credentials
│   └── CREDS/               # Matched keyword files (password.txt, etc.)
└── statistics.txt           # Final session report
Final Report
The statistics.txt file includes:

Total execution time.

List of tools used.

Directory tree of generated evidence.

Summary of extracted network traffic and PCAP files.

⚠️ Disclaimer
This tool is created for educational purposes and authorized forensic investigations only. The author is not responsible for any misuse or damage caused by this software. Ensure you have proper authorization before analyzing any data.

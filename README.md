# 🛡️ Mastering File Server Resource Manager (FSRM): Taming the Beast with Quotas and File Screens

Welcome to Phase 2 of my Windows Server 2025 Homelab! In this module, I implemented **File Server Resource Manager (FSRM)**. 

While standard NTFS permissions control *who* can access a folder, FSRM controls *what* they can do inside it. This lab focuses on two critical enterprise features:
1. **Quotas:** Preventing a single department from accidentally filling up the entire server hard drive.
2. **File Screening:** Blocking unauthorized file types (like personal music or unapproved executables) from being stored on corporate servers.

---

## 🛠️ Step 1: Installing the FSRM Role
FSRM is not installed by default. I added it via the Server Manager using the Add Roles and Features Wizard.

<img width="1166" height="685" alt="Image" src="https://github.com/user-attachments/assets/76f4c295-2b18-48b3-8429-3a20d1fd8613" />

---

## 📊 Feature 1: Setting Up a Hard Quota
To test this, I applied a strict **2 GB Hard Quota** to the HR Department share (`C:\Shares\HR-shares`). 
*   **Hard Quota:** Once the 2 GB limit is reached, users are physically blocked from saving new data.
*   **Soft Quota:** (Alternative) Only sends an alert but allows users to exceed the limit.

### Configuring the Quota:
I navigated to `Quota Management` > `Quotas` and created a new quota using the built-in 2 GB template.

<img width="1155" height="691" alt="Image" src="https://github.com/user-attachments/assets/11e598be-1e63-44cb-a51f-0c9424a6824d" />

### The Active Quota View:
Once created, the quota is active. If the HR department hits this limit, they will receive a "Disk Full" error, even if the server has terabytes of free space remaining.

<img width="1165" height="688" alt="Image" src="https://github.com/user-attachments/assets/e8268d4d-84d7-48ae-ac8c-daf8b6e19d76" />

---

## 🚫 Feature 2: Active File Screening
Next, I locked down the HR share to prevent users from using the server as a personal media drive. 

### Creating the File Screen:
I applied an **Active File Screen** using the "Block Audio and Video Files" template. 
*   **Active:** Blocks the file from being saved.
*   **Passive:** Allows the file to be saved, but logs an event (useful for monitoring before enforcing).

<img width="1161" height="688" alt="Image" src="https://github.com/user-attachments/assets/cf00c66f-4b76-4688-b255-1eeb6519a262" />

### Customizing the File Groups:
I went a step further and customized the blocked file groups. In addition to Audio and Video, I blocked **Executable Files** and **Image Files** to prevent users from storing unvetted software installers or massive photo albums on the file server.

<img width="1169" height="684" alt="Image" src="https://github.com/user-attachments/assets/360456b8-7501-4e19-b62b-f543be81c07c" />

### The Final Active Screen:
The file screen is now live. Any attempt to copy a `.mp3`, `.mp4`, `.exe`, or `.jpg` into the HR share will be instantly intercepted and denied by Windows.

<img width="1166" height="685" alt="Image" src="https://github.com/user-attachments/assets/980ef853-35d7-48aa-a25c-0f34a34e5577" />

---

## 💡 Key Takeaway
**NTFS handles Security. FSRM handles Operations.** 
By combining strict NTFS permissions with FSRM quotas and file screens, you build a resilient file server that protects both its data and its storage capacity.

*Next up: Configuring Shadow Copies (Previous Versions) so users can restore their own deleted files!*

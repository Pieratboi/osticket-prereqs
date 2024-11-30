
<p align="center">
<img src="https://i.imgur.com/Clzj7Xs.png" alt="osTicket logo"/>
</p>

# osTicket - Prerequisites and Installation
This documentation outlines the prerequisites and step-by-step process to install and configure the open-source help desk ticketing system, **osTicket**. This project demonstrates the installation and set-up of osTicket in a cloud-hosted environment.

osTicket is a powerful, open-source solution for managing customer support tickets efficiently. The system centralizes inquiries and automates processes, making it ideal for IT service desks, customer service departments, and small businesses looking for a cost-effective ticketing solution.

---

## Table of Contents
1. [Environments and Technologies Used](#environments-and-technologies-used)
2. [Operating System Used](#operating-system-used)
3. [Prerequisites](#prerequisites)
4. [Installation Steps](#installation-steps)
    - [Set Up the Virtual Machine](#1-set-up-the-virtual-machine)
    - [Enable Internet Information Services (IIS)](#2-enable-internet-information-services-iis)
    - [Install osTicket Dependencies](#3-install-osticket-dependencies)
    - [Configure IIS](#4-configure-iis)
    - [Install osTicket](#5-install-osticket)
    - [Complete the osTicket Web-Based Setup](#6-complete-the-osticket-web-based-setup)
5. [Troubleshooting](#troubleshooting)
6. [Access Points](#access-points)
7. [Licensing Information](#licensing-information)
8. [Contact Information](#contact-information)

---

## Environments and Technologies Used

- **Microsoft Azure**: Cloud platform used to host a Windows 10 Virtual Machine (VM) for the installation.
- **Windows 10**: Operating system providing the environment for installing the required software stack.
- **Internet Information Services (IIS)**: Microsoft's web server used to host and serve the osTicket application.
- **PHP**: A widely-used server-side scripting language required for osTicket's backend processing.
- **MySQL**: A relational database management system to store and manage osTicket's data.
- **HeidiSQL**: A graphical tool for managing MySQL databases.

---

## Operating System Used

- **Windows 10 Pro** (Version 21H2)

---

## Prerequisites

Before starting, ensure you have:

1. **A Virtual Machine**:
   - Create a Windows 10 Virtual Machine with at least:
     - 4 vCPUs
     - 8 GB RAM
     - Internet connectivity for downloading and installing dependencies.

2. **osTicket Installation Files**:
   - Download the `osTicket-Installation-Files.zip`, containing all the required dependencies for setting up osTicket.

3. **Administrative Access**:
   - Ensure you have administrative privileges to install and configure software on the VM.

4. **Software to Be Installed**:
   - **Internet Information Services (IIS)** with CGI enabled:
     - A web server required to host the osTicket web application.
   - **PHP Manager for IIS**:
     - A tool for managing PHP configurations within IIS.
   - **Rewrite Module**:
     - An IIS component used for URL rewriting and redirection, necessary for clean URLs in osTicket.
   - **PHP** (Version 7.3.8):
     - Required for server-side scripting and executing osTicket's backend code.
   - **VC_redist.x86.exe**:
     - The Visual C++ Redistributable provides runtime components needed for applications written in C++.
   - **MySQL 5.5.62**:
     - A database server used to store osTicket's data, such as tickets, users, and settings.
   - **HeidiSQL**:
     - A GUI tool to connect to and manage MySQL databases.

---

## Skills and Tools Demonstrated

- **Cloud Infrastructure Management**: Configuring a virtual machine using Microsoft Azure.
- **Web Server Configuration**: Installing and managing IIS to serve web applications.
- **Database Administration**: Setting up and managing a MySQL database for osTicket.
- **Scripting and Automation**: Integrating PHP with IIS and configuring necessary extensions.
- **Troubleshooting**: Identifying and resolving installation and configuration issues.
- **System Security**: Applying best practices for file permissions and access controls.

---

## Installation Steps

![image](https://github.com/user-attachments/assets/8aae0d8d-b165-448d-ba73-df3ea7f84cb7)


### 1. Set Up the Virtual Machine
- Create a Windows 10 Virtual Machine in Microsoft Azure or another platform of your choice.
- Ensure the VM has sufficient resources (4 vCPUs, 8GB RAM, and a public IP address for remote access).

### 2. Enable Internet Information Services (IIS)
- IIS will serve as the web server for the osTicket application.
- Steps:
  1. Open **Control Panel** > **Programs** > **Turn Windows features on or off**.
  2. Enable:
     - **Internet Information Services (IIS)**.
     - **World Wide Web Services** → **Application Development Features** → **CGI**.

### 3. Install osTicket Dependencies
1. **Install PHP Manager for IIS**:
   - Simplifies PHP integration with IIS.
   - Run `PHPManagerForIIS_V1.5.0.msi` from the installation files.

2. **Install IIS Rewrite Module**:
   - Enables advanced URL rewriting for clean URLs.
   - Run `rewrite_amd64_en-US.msi`.

3. **Set Up PHP**:
   - Create a directory `C:\PHP`.
   - Extract PHP binaries (`php-7.3.8-nts-Win32-VC15-x86.zip`) into `C:\PHP`.

4. **Install Visual C++ Redistributable**:
   - Run `VC_redist.x86.exe`.

5. **Install MySQL Database Server**:
   - Run `mysql-5.5.62-win32.msi`.
   - Use the **Typical Setup**.
   - Launch the **Configuration Wizard**:
     - Use **Standard Configuration**.
     - Set a root username and password.

### 4. Configure IIS
- Open IIS as Administrator.
- Register PHP with IIS:
  - Use **PHP Manager** to register `C:\PHP\php-cgi.exe`.
- Restart IIS.

### 5. Install osTicket
1. Extract `osTicket-v1.15.8.zip`.
2. Copy the `upload` folder to `C:\inetpub\wwwroot`.
3. Rename `upload` to `osTicket`.
4. Restart IIS.

### 6. Complete the osTicket Web-Based Setup
1. Navigate to `http://localhost/osTicket`.
2. Enable required PHP extensions in IIS:
   - `php_imap.dll`, `php_intl.dll`, `php_opcache.dll`.
3. Rename `ost-sampleconfig.php` to `ost-config.php` and configure permissions.
4. Set up the MySQL database and complete the web-based setup.

![image](https://github.com/user-attachments/assets/42f6a171-2211-4252-8ce5-bcb24be1be65)

---

## Troubleshooting

1. **Issue**: "HTTP Error 500.0 - Internal Server Error" when accessing osTicket.  
   - **Cause**: PHP is not properly registered, or a required extension is missing.  
   - **Solution**: Re-register PHP in IIS Manager and ensure all required extensions are enabled.

2. **Issue**: "Database connection failed" during web setup.  
   - **Cause**: Incorrect MySQL credentials or database name.  
   - **Solution**: Verify credentials and ensure the database exists in HeidiSQL.

3. **Issue**: Permissions error for `ost-config.php`.  
   - **Cause**: File permissions are not correctly configured.  
   - **Solution**: Disable inheritance, remove existing permissions, and grant full control to `Everyone`. Set the file to read-only after setup.

---

## Access Points
- **Admin Panel**: [http://localhost/osTicket/scp/login.php](http://localhost/osTicket/scp/login.php)
- **Client Portal**: [http://localhost/osTicket/](http://localhost/osTicket/)

---

## Licensing Information
osTicket is distributed under the GNU General Public License (GPL). For more information, visit the [osTicket License](https://osticket.com).

---

## Contact Information
For questions or feedback, feel free to reach out:  
- **GitHub**: https://github.com/Pieratboi  
- **LinkedIn**: <a href="https://www.linkedin.com/in/rafael-razapov-60391a2b8/?trk=opento_sprofile_topcard"> Rafael Razapov </a>  

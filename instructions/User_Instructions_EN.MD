# 🛡️ User Guide: MyFirewall

## Introduction
MyFirewall is a privacy protection and network control solution for Android. It allows you to block advertisements and trackers, and precisely control Internet access for every application installed, whether your device is rooted or not.

---

## 🔑 Permissions (Onboarding Screen)
During the initial setup, MyFirewall requires several critical authorizations to function:

*   **VPN Service (Local)**: Used to intercept traffic without sending your data to an external server.
*   **Usage Statistics (Optional)**: Allows the app to identify which application is consuming data in real-time.
*   **Notifications**: Essential for keeping the service active in the background and alerting you in case of disconnection.
*   **Root Access (Optional)**: Enables low-level filtering via the system `hosts` file, providing better performance and zero battery consumption.

---

## 1. Dashboard Screen (Status)
This screen centralizes the status of your protection.

*   **Monitoring**: View the number of blocked applications and the current traffic speed (Upload/Download).
*   **Rule Cards (URL Filters)**:
    *   **Long-press**: Instantly toggle a filtering category (Ads, Social Media, etc.) directly from the dashboard without going through settings.

---

## 2. Applications Screen
Manage the network access rights for each application individually.

### 2.1 Categories and Quick Filters
*   **Filter Icons**: At the top of the list, icons allow you to isolate applications (All, System, User, Internet Access, No Internet Access).
*   **Long-press on a filter icon**: Quickly select or deselect all applications corresponding to that filter for bulk management.

### 2.2 Control Per Application
*   **Click on the app icon**: Opens the system properties for the application (to clear cache or force stop).
*   **Long-press on the app name**: Instantly toggles all connectivity (ON/OFF). If the app was allowed, it becomes fully blocked, and vice versa.
*   **Traffic Icon Functions**:
    *   🌐 **Wi-Fi**: Allow/Block access when on a wireless network.
    *   📶 **Mobile Data**: Allow/Block access on 4G/5G networks.
    *   ✈️ **Roaming**: Specifically block access when abroad to avoid overage charges.

---

## 3. Rules Screen (Filtering by Domain Name)
Configure your DNS blocking engine.

### 3.1 List Selection (Presets)
*   **Provenance**: Lists come from recognized sources (StevenBlack, AdAway).
*   **Updates**: MyFirewall periodically checks for list freshness. You can force a manual update to get the latest reported malicious domains.

### 3.2 User Blocklist (Manual Editing)
*   **Editing**: Write, copy, or paste your own domains to block in the text field (one per line).
*   **Clear Button**:
    *   *Simple Tap*: Clears the current text field for new input.
    *   The **Configure** button reloads rules currently stored in the database back into the editor.
    *   *Via Dropdown Menu*: Allows you to permanently delete all custom rules stored in the database.
*   **Local Export**: Use the dedicated buttons to export your rules to a `.txt` file.

### 3.3 Import / Export Screen (Global)
*   **Export Button**: Saves your entire configuration.
    *   **Dropdown Menu**: Allows you to selectively export either application rules (Firewall) or URL filter lists.
*   **Import Button**: Follows the same logic to selectively restore your settings from a previous backup.

---

## 4. Settings Screen
The technical configuration core.

### 4.1 Non-Rooted Devices
On these devices, filtering uses the local VPN engine.
*   **Exclusivity**: URL filtering and Application filtering are exclusive. You must choose which engine takes priority for managing the VPN tunnel.

### 4.2 Rooted Devices
*   **Cumulative**: Rules are cumulative. You can use the **Hosts** engine for URL filtering (DNS) and the **VPN** engine for application filtering, offering a high-performance double-layer protection.

### 4.3 Custom DNS Server
*   **Non-Root**: You can specify a custom DNS server (e.g., Cloudflare, Quad9) directly within the application.
*   **Root**: DNS must be set directly in Android system settings to use a custom DNS server.

### 4.4 Notifications and Hosts Filtering
*   **Hosts URL Filtering**: A dedicated service handles secure writing to the system hosts file or Magisk's systemless hosts.
*   **Independence**: Once the `hosts` file is written by MyFirewall, blocking becomes native. Even if the app is closed or uninstalled, the Android system will continue to block domains, which is the most battery-efficient method.
* To avoid being left with a modified hosts file (for example, if the app is uninstalled), a notification is provided to warn the user that hosts-based protection is active. To allow this notification to display, it is necessary to disable battery optimization to allow unrestricted background use of the application, so the notification service is not killed.

---

## 5 MyFirewall for Advanced Users

### 5.1 Use with a Third-Party VPN (e.g., NordVPN, ProtonVPN)
Android has a software limitation: **only one VPN service can be active at a time** across the entire system. Since MyFirewall uses a local VPN for application and URL filtering (on non-rooted devices), launching a commercial VPN will automatically disable MyFirewall's protection.

*   **Non-Rooted Devices:** You must choose between MyFirewall protection or your commercial VPN. They cannot run simultaneously.
*   **Rooted Devices:** This is the recommended mode for third-party VPN users. By using the **Hosts** engine for URL filtering, MyFirewall does not use the Android VPN service. You can therefore benefit from MyFirewall's ad-blocking **AND** your usual VPN's secure connection at the same time.

### 5.2 About Presets
* Several features offer presets (filtering rules and DNS servers). If you do not wish to use them, simply disable them and use your own preferences instead. In this case, the application's only network activity will be filtering URLs and blocking application traffic.

### ⚠️ Important Note for Root Users
If you decide to uninstall MyFirewall, it is **imperative** to follow these steps to restore your system to its original state:

1.  **Disable all blocklists** (Presets and User Blocklist) in the "Rules" tab.
2.  **Disable "URL Filtering (Hosts)"** in the "Settings" screen.
3.  This action triggers the cleanup routine that **restores your device's original `hosts` file**.

*Note: If you uninstall the application without performing these steps, advertising domains will remain blocked indefinitely on your device, as the modification to the system file is permanent.*

---
*MyFirewall - Your privacy, your rules.*

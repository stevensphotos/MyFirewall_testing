# MyFirewall

## IMPORTANT NOTE
-** This repository is intended to test my new application. It is aimed at users conducting functionality and stability tests. Once the application has been tested and deemed satisfactory, the source code will be released.

MyFirewall is a powerful, privacy-focused network security application for Android. It acts as a local gatekeeper, giving you total control over which applications can access the internet and blocking unwanted content at the source.

## 🛡️ Key Features

- **Application Firewall**: Selectively allow or block internet access for each app based on your connection type (Wi-Fi, Mobile Data, or Roaming).
- **DNS/URL Filtering**: Block ads, trackers, and malicious domains using a high-performance local VPN tunnel.
- **Root Mode (Hosts Filter)**: For advanced users, MyFirewall can modify the system hosts file for zero-battery impact and system-wide protection.
- **Privacy First**: All filtering happens locally on your device. No traffic data ever leaves your phone or is sent to external servers.
- **Material 3 Design**: A modern interface supporting Dark Mode, Dynamic Colors, and specialized "Pure Black" for AMOLED screens.

## 🚀 Quick Start Guide

1. **Installation**: Install the APK on your Android device (Android 8.0+).
2. **Setup**: Follow the onboarding guide to grant necessary permissions (VPN and Notifications).
3. **Protection**:
    - Navigate to the **Apps** tab to configure your firewall rules.
    - Go to the **Rules** tab to enable ad-blocking presets.
4. **Monitor**: Check the **Dashboard** for real-time traffic statistics and blocked requests.

> [!IMPORTANT]
> For a complete guide on features, DNS configuration, and specific instructions for Root users, please refer to our **[Detailed User Instructions](instructions/User_Instructions_EN.MD)**.


## 🔧 Technical Details

- **Local VPN Tunnel**: Uses Android's `VpnService` to create a virtual network interface.
- **Isolated Network**: Implements a restricted `/30` subnet (`255.255.255.252`) to prevent IP conflicts with your local Wi-Fi.
- **Packet Interception**: Only DNS requests (UDP 53) are intercepted for filtering, ensuring minimal impact on network latency.
- **Battery Optimization**: The app is designed to avoid unnecessary CPU wake-ups. Root mode offers the most efficient filtering path.

## ❓ FAQ

**Is my data safe?**  
Yes. MyFirewall does not collect, store, or transmit your browsing history. All analysis is done on-device.

**Why is there a VPN icon?**  
Android requires a VPN interface to allow any non-root app to filter network traffic. It is a local "dummy" VPN, not a remote proxy.

**Does it drain the battery?**  
The impact is minimal. For maximum efficiency, users with Root access can use the Hosts-based filter.

## 📜 License

MyFirewall is released under the **GPLv3 License**. You are free to view, modify, and contribute to the source code to ensure the security and transparency of the project.

---
*Developed with rigor and stability in mind.*

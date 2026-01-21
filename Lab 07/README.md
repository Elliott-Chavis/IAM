# Lab 07: Device Compliance, App Protection & Shared PC Mode (2026 Edition)

This lab covers the end-to-end implementation of device security and data protection for **MSA Contractors** using Microsoft Intune and Entra ID. It includes hardware lockdown ("Library Mode"), mobile app security (MAM), and 2026 connectivity standards.

---

## 🛠 Prerequisites & Initial Setup

### Step 0: License & Identity Preparation
Before beginning, ensure the tenant has the necessary 2026 licenses assigned.

1. **Activate Trial:** Navigate to **M365 Admin Center** > **Marketplace**. Search for **Microsoft Intune Plan 1** and start the free trial.
2. **Assign License:** Go to **Users** > **Active users** > Select your **Global Admin** account. 
3. **Configuration:** Under **Licenses and apps**, check **Intune Plan 1** and save.
   > [!IMPORTANT]
   > Ensure your **Usage Location** (e.g., United States) is set in your user profile properties, or the Intune license cannot be assigned.

### Step 1: Create the Lab Device Group
We use a dedicated device group to target hardware-specific "Library Mode" settings without affecting personal devices.

1. **Path:** [Entra ID Portal](https://entra.microsoft.com/) > **Groups** > **All groups** > **New group**.
2. **Details:**
   - **Group type:** Security
   - **Group name:** `LAB-WIN-ManagedDevices`
   - **Membership type:** Dynamic Device
3. **Dynamic Rule:** Click **Add dynamic query** > **Edit** and paste:
   ```sql
   (device.displayName -startsWith "LAB-") -and (device.deviceOSType -eq "Windows")

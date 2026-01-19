# Azure IAM Beginner Lab 06: Implementing Entra ID Protection (2026 Edition)

### **Modern 2026 Entra ID Workflow Active**
* **Identity Platform:** Microsoft Entra ID (Formerly Azure AD).
* **Licensing:** **Entra ID P2** Required (Currently Active).
* **Security Standard:** Zero Trust Adaptive Defense.
* **Key Update:** Legacy "Identity Protection" sliders are retiring **October 1, 2026**. This lab follows the modern **Conditional Access** integration.

---

## **Objective**
Configure an AI-driven "Adaptive" defense that automatically responds to user and sign-in risks using trillion-signal intelligence from Microsoft.

---

## **Phase 1: Intelligence Discovery (The Dashboard)**
Before blocking users, we must analyze the "Threat Landscape" detected by Entra AI.

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Navigate to **Entra ID** > **ID Protection** > **Dashboard**.
3. **Analyze Metrics:**
    * **Attack Graphic:** View visual representations of common attacks (Password Spray, etc.).
    * **Risky Locations:** Check the map for suspicious geographic sign-in patterns.
4. **Setup Alerts:**
    * Go to **Notify** > **Users at risk detected alerts**.
    * Set **Alerting** to **Enabled**.
    * Add your email to the **Recipients** list.
    * Click **Save**.

---

## **Phase 2: Pre-Requisite (Disable Security Defaults)**
You cannot use granular Conditional Access policies while the "all-or-nothing" Security Defaults are active.

1. Navigate to **Entra ID** > **Overview** > **Properties**.
2. Scroll to the bottom and click **Manage security defaults**.
3. Set **Security defaults** to **Disabled**.
4. **Reason:** Select "My organization is using Conditional Access" and click **Save**.

---

## **Phase 3: MFA Registration Enforcement**
*Self-remediation* (letting a user fix their own risk) requires MFA to be set up **before** they are flagged.

1. Navigate to **Entra ID** > **ID Protection** > **Multifactor authentication registration policy**.
2. **Assignments:** * Click **All users** > Switch to **Select individuals and groups**.
    * Click **Users and groups** > **Select users and groups**.
    * Search for and select your **Test User**.
3. **Controls:** Ensure **Require Microsoft Entra MFA registration** is checked.
4. **Policy enforcement:** Set to **Enabled** and click **Save**.

---

## **Phase 4: Create User Risk Policy (Conditional Access)**
This handles "Offline Detections" like a user's password appearing on a dark-web dump.

1. Navigate to **Entra ID** > **Conditional Access**.
2. Click **+ New policy** and name it: `[IDP-01] User Risk Remediation`.
3. **Assignments:**
    * **Users:** Choose **Select users and groups** > **Users and groups**.
    * Search for and select your **Test User**. (Ensure your Break-glass admin is **Excluded**).
4. **Target resources:** Select **All resources**.
5. **Conditions:**
    * Select **User risk** > Set to **Yes** > Select **High**.
6.  **Access controls (Grant):**
    * Select **Grant access**.
    * Select **Require password change**.
7. **Enable policy:** Set to **On** and click **Create**.

---

## **Phase 5: Create Sign-in Risk Policy (Conditional Access)**
This handles "Real-Time" threats like a login from a Tor browser or an "Impossible Travel" event.

1. In **Entra ID** > **Conditional Access**, click **+ New policy**.
2. Name it: `[IDP-02] Sign-in Risk Challenge`.
3. **Assignments:** Repeat the same selection path to include your **Test User**.
4. **Conditions:**
    * Select **Sign-in risk** > Set to **Yes** > Select **High** and **Medium**.
5. **Access controls (Grant):**
    * Select **Grant access**.
    * Select **Require multifactor authentication**.
6. **Enable policy:** Set to **On** and click **Create**.

---

## **Troubleshooting Guide**

| Symptom | Potential Cause | 2026 Resolution |
| :--- | :--- | :--- |
| **"Policy cannot be enabled"** | Security Defaults are still On. | Re-verify Step 2: **Entra ID > Properties > Manage security defaults** must be Disabled. |
| **User is blocked instantly** | MFA not registered. | Ensure the user has completed registration (Step 3). High-risk users are blocked if they can't perform MFA. |
| **Menu is missing** | 2026 UI Collapse. | Use the Global Search bar at the top and type **"Conditional Access"** to jump straight there. |
| **Policies not firing** | Trusted Location/IP. | Check **Named Locations**. Risk-based policies may skip triggers if you are on a network marked as "Trusted." |

---

## **Lab 06 Q&A**

**Q: Why do we disable Security Defaults?**
**A:** Security Defaults is a free "starter pack." Once you have a P2 license, you must disable it to use **Conditional Access**, which offers granular rules (like excluding your break-glass account).

**Q: What is the difference between User Risk and Sign-in Risk?**
**A:** **User Risk** is about the account (offline, like a leaked password). **Sign-in Risk** is about the session (real-time, like a suspicious IP address).

**Q: Why migrate away from the old ID Protection menu sliders?**
**A:** Microsoft is consolidating all "Access Enforcement" into **Conditional Access**. The old sliders are being retired in late 2026.

---

## **Verification Task**
1. Open a **Private/Incognito** window and log in as your Test User.
2. Complete the MFA registration (triggered by Phase 3).
3. In the admin portal, go to **Entra ID** > **ID Protection** > **Risky Users**.
4. Find your user and select **"Confirm user compromised."** (This manually spikes their risk level).
5. Attempt to log in again. You should be blocked until you complete a **secure password reset**!

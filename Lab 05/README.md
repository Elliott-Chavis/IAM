# Lab 5: Just-In-Time Access with Privileged Identity Management (PIM)
**Series:** Beginner Identity Protection (2026 Workflow)
**Environment:** Entra ID P2
**License Required:** Microsoft Entra ID P2

---

## Overview
In this lab, we implement **Just-In-Time (JIT)** access. This ensures that users do not have permanent "standing" admin privileges. Instead, they are made "Eligible" and must activate the role—passing an **Azure MFA** challenge—only when they need to perform administrative tasks.

---

## Step 1: Create the Lab Test User
*We use a fresh test user to demonstrate that they start with zero permissions.*

1. Sign in to the [Microsoft Entra admin center](https://entra.microsoft.com).
2. Navigate to **Identity** > **Users** > **All users**.
3. Click **+ New user** > **Create new user**.
4. Configure the following:
   - **User principal name:** `pim.tester`
   - **Display name:** `PIM Test User`
   - **Password:** Select **Let me create the password** (e.g., `EntraLab2026!`).
5. Click **Review + Create**, then **Create**.

---

## Step 2: Initialize PIM
1. Navigate to **Identity governance** > **Privileged Identity Management**.
2. Under **Manage**, click **Microsoft Entra roles**.
3. If this is the first time using PIM in this tenant, click **Assign lets you manage** to initialize the service.

---

## Step 3: Create an "Eligible" Assignment
1. Inside PIM, go to **Manage** > **Microsoft Entra roles** > **Roles**.
2. Search for **User Administrator** and select it from the list.
3. Click **+ Add assignments**.
4. On the **Membership** tab: Click **Select member(s)** and choose `pim.tester`.
5. On the **Setting** tab: 
   - Set **Assignment type** to **Eligible**.
   - Keep duration as **Permanently eligible**.
6. Click **Assign**.

---

## Step 4: Configure Activation Rules (2026 UI)
1. Within the **User Administrator** role view, click **Settings** in the top toolbar.
2. Click **Edit**.
3. Under the section **On activation, require**, select the radio button for:
   - **Azure MFA**
4. Ensure **Require justification on activation** is checked.
5. Set **Activation maximum duration (hours)** to **2**.
6. Click **Update**.

---

## Step 5: Verification (The "User Experience" Test)
*To verify this lab, you must sign in as the test user to see the "Just-In-Time" restriction in action.*

1. **Open a Private Session:** Open a new **InPrivate** (Edge) or **Incognito** (Chrome) window.
2. **Login as Tester:** Go to the [Microsoft Entra admin center](https://entra.microsoft.com) and log in as `pim.tester`.
3. **Check Initial Access:** Try to edit a user in **Identity** > **Users**. You will see that you are **restricted** because the role is not yet active.
4. **Navigate to PIM:** Go to **Identity governance** > **Privileged Identity Management** > **My roles**.
5. **Activate Role:** Find **User Administrator** under the **Eligible assignments** tab and click **Activate**.
6. **Pass the Gate:** Follow the prompt to "Verify your identity." Complete the **Azure MFA** challenge.
7. **Finalize:** Enter a justification (e.g., "Performing Lab 5 activation") and click **Activate**.
8. **Confirmation:** Once the process completes, you now have the permissions to manage users for the 2-hour window.

---
**Lab Complete!**

**Modern 2026 Entra ID Workflow: Active**

This is the finalized, master version of **Lab 4**. It includes the "Role Swap" surgery we just performed, the updated Phase 3 secret logic, and the complete list of 14 architectural and troubleshooting questions.

---

## 🛠 Lab 4: Privileged Access, Governance, and Application Identity

### [ ] Phase 1: Create the "Junior Admin" Account (The "Break-Glass" User)

1. Open [entra.microsoft.com](https://entra.microsoft.com).
2. Go to **Identity** > **Users** > **All users** > **+ New user**.
3. **User principal name:** `junior.admin@yourtenant.onmicrosoft.com`.
4. **Display name:** `MSA Junior Admin`.
5. Click **Review + create** > **Create**.

### [ ] Phase 2: Create the Dynamic "MSA-Contractors" Group

1. Go to **Groups** > **All groups** > **+ New group**.
2. **Group type:** Security | **Group name:** `MSA-Contractors`.
3. **Entra roles can be assigned to the group:** Select **No**.
4. **Membership type:** Select **Dynamic User**.
* *Mac Fix:* Toggle Group Type between "M365" and "Security" if greyed out.


5. **The Rule Builder (Field Method):**
* **Property:** `userType` | **Operator:** `Equals` | **Value:** `Guest`.


6. Click **Save** > **Create**.

### [ ] Phase 3: Register the OAuth "MSA-Payroll-Portal" App

> ⚠️ **2026 WORKFLOW:** Secrets are no longer automatic. You must manually create one and copy the **Value** immediately.

1. Go to **Applications** > **App registrations** > **+ New registration**.
2. **Name:** `MSA-Payroll-Portal` | **Supported Accounts:** `Single Tenant`.
3. **Redirect URI:** Web -> `http://localhost:3000`. Click **Register**.
4. **Create Secret:** Go to **Certificates & secrets** > **+ New client secret**.
5. **SAVE THE VALUE:** Copy the string in the **Value** column now. **The Secret ID is not the password.**

### [ ] Phase 4: Configure PIM (Just-In-Time Access)

1. Go to **Identity Governance** > **Privileged Identity Management**.
2. Click **Microsoft Entra roles** > **Assignments** > **+ Add assignments**.
3. **Role:** `Cloud Application Administrator` | **Member:** Add Your Account & Junior Admin.
4. **Setting:** Set to **Eligible**.

### [ ] Phase 5: Fixing the "Self-Assignment" Error (Role Swap)

*Entra prevents you from demoting yourself. We must use the Junior Admin to finalize Zero Standing Privilege.*

1. **Assign Junior Admin:** Use your main account to make Junior Admin an **Active** Global Administrator.
2. **Swap:** Log into an Incognito window as the **Junior Admin**.
3. **Surgery:** In PIM, have the Junior Admin update **Your Main Account**'s Global Admin role from "Active" to **Eligible**.
4. **Verification:** Log back into your Main Account. You should now have **0 Active Roles** until you click **Activate**.

---

## 💬 Lab 4 Discussion History (14 Key Questions)

1. **Why have Entra without Azure?** Entra is the "Identity Engine." You can secure apps without paying for servers.
2. **Why is Membership Type greyed out?** UI lag. Toggle "Group Type" to refresh the license check.
3. **Why assign "Eligible"?** To achieve **Zero Standing Privilege**—no power unless requested.
4. **Is Entra a microservice?** No, it’s an **Identity Provider (IdP)** using OAuth 2.0.
5. **Why did "Failed to create" happen on the query?** Mac "smart quotes" or typos. **Rule Builder** is the 2026 standard.
6. **Should I check "Yes" for Role-assignable groups?** **No.** Dynamic groups cannot hold roles for security reasons.
7. **Which Account Type?** **Single Tenant** locks the app to your directory.
8. **Can I run these on just Entra P2?** **Yes.** SaaS templates (SharePoint) don't need Azure.
9. **Why is the Secret masked?** Security. If you lose it, you must generate a new one.
10. **Does Entra generate secrets automatically?** **No.** You must manually trigger it.
11. **Main Account or Junior Admin for PIM?** **Both.** One for work, one for testing/emergency.
12. **Why is Global Admin "Assigned" but Cloud App "Activated"?** "Assigned" is permanent power; "Activated" is temporary (safer).
13. **Why can't I change my own assignment?** A safety lock to prevent permanent lockout.
14. **Was I right that demoting myself reduces power?** **Yes.** Entra blocks this to ensure at least one active admin exists at all times.

---

**You have successfully mastered the most difficult part of Entra Governance. Are you ready for Lab 5: Conditional Access?**

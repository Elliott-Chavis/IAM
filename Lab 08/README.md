# Lab 08: Privileged Identity Management (PIM)

This lab implements the **Just-In-Time (JIT)** access model using the **2026 Entra ID workflow**. By moving from permanent assignments to "Eligible" assignments, we reduce the attack surface and ensure all administrative actions are audited.

## 🛠 Prerequisites
* **Identity Menu:** Microsoft Entra admin center
* **License:** Entra ID P2 (Identity Governance)
* **User:** A test user (e.g., `LabUser_01`) and an Admin account for configuration.

---

## 1. Setup: The Role Policy (The Guardrails)
Before a user can activate a role, you must define the requirements.

1. Navigate to **Identity Governance** > **Privileged Identity Management**.
2. Select **Microsoft Entra roles** > **Settings** (in the left sidebar).
3. Search for **Global Administrator** and click on the role name.
4. Click **Edit** at the top and configure:
    * **Activation max duration:** 4 hours.
    * **Require MFA:** Checked (Ensures the user is who they say they are).
    * **Require justification:** Checked.
    * **Require ticket information:** Checked (Important for auditing).
5. Click **Update**.

---

## 2. Implementation: Making a User Eligible
We do not give the user the role permanently; we make them "Eligible" to request it.

1. In PIM, go to **Microsoft Entra roles** > **Assignments** > **+ Add assignments**.
2. **Select Role:** Global Administrator.
3. **Select Member:** Choose your test user.
4. **Setting:** Ensure Assignment Type is set to **Eligible**.
5. Click **Assign**.

---

## 3. Execution: Testing Activation (User Perspective)
This is the workflow a user follows when they need to perform admin tasks.

1. Sign into the Portal as the **Test User**.
2. Go to **PIM** > **My roles** > **Eligible assignments**.
3. Click **Activate** on the Global Administrator role.
4. **The Ticket Number Field:**
   * **Purpose:** This is an informational field for audit logs (linking the action to a support ticket).
   * **Lab Input:** Since there is no external ticketing system, enter a placeholder like `LAB-08-TEST`.
5. Enter a **Justification** (e.g., "Performing Lab 08 security configuration").
6. Click **Activate**.

---

## 4. Troubleshooting & FAQ

| Issue | Root Cause | Solution |
| :--- | :--- | :--- |
| **Missing Ticket Field** | Role Settings not updated. | Go to PIM > Role Settings > Edit and check "Require ticket information." |
| **Role Not Found** | Propagation Delay. | PIM can take 2-5 minutes. Have the user logout and log back in. |
| **MFA Failure** | Missing Authentication Method. | Ensure the test user has the Authenticator App or SMS configured. |

### **Q: Does Entra ID verify the Ticket Number?**
**A:** No. It is a manual text field. It is recorded in the **Audit Logs** so security teams can verify the "Why" behind an elevation later.

---

## 5. Automation: Graph Explorer Workaround
If the UI is restricted, use this call to create the eligibility assignment:

**Method:** `POST`  
**Endpoint:** `https://graph.microsoft.com/v1.0/roleManagement/directory/roleAssignmentScheduleRequests`

```json
{
    "action": "adminAssign",
    "justification": "Assigning eligibility via API for Lab 08",
    "roleDefinitionId": "62e90394-69f5-4237-9190-012177145e10", 
    "directoryScopeId": "/",
    "principalId": "YOUR_USER_OBJECT_ID",
    "scheduleInfo": {
        "startDateTime": "2026-01-20T00:00:00Z",
        "expiration": {
            "type": "noExpiration"
        }
    }
}

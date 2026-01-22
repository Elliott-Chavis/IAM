# Lab 10: Entra ID Identity Protection
**Current Environment:** 2026 Entra ID Workflow | **License:** Entra ID P2

---

## Lab Objectives
1.  **Protect Admin Access:** Exclude your Global Admin from strict policies using its **Object ID**.
2.  **Deploy RBCA Policies:** Implement the 2026 Risk-Based Conditional Access (RBCA) standard.
3.  **Automate Alerts:** Set up real-time email notifications for high-risk detections.
4.  **Simulate Compromise:** Use Microsoft Graph Explorer to manually flag a test identity.
5.  **Verify Enforcement:** Confirm the remediation flow triggers for the "Compromised" user.

---

## Step 1: Secure Your Admin Access
Before applying global security rules, you must identify your "Safety Net."
1.  Sign in to the **Microsoft Entra admin center**.
2.  Navigate to **Identity** > **Users** > **All users**.
3.  Locate your admin account and copy the **Object ID**.
4.  **Why?** In the next step, we use "All Resources." Excluding your specific Object ID ensures you don't accidentally block your own access if a policy is misconfigured.

---

## Step 2: Configure Risk Remediation Policies (RBCA)
In 2026, legacy standalone policies are replaced by the RBCA engine within Conditional Access.

### Policy A: User Risk (Compromised Credentials)
1.  Navigate to **Protection** > **Identity Protection** > **RBCA**.
2.  Select **+ New policy** > Name: `LAB10-UserRisk-Remediation`.
3.  **Assignments**: 
    * **Include:** All users

**Modern 2026 Entra ID Workflow: Active**

Since you now have the **P2 License**, we no longer need to "simulate" automation with the Graph API. We can now use the native **Entra Dynamic Membership Engine**. This is the professional way to handle identity at scale, allowing the "System" to do the work you previously did manually with API calls.

---

## 🛠 Lab 2: Automated Identity Governance (P2 Dynamic Groups)

### [ ] Phase 1: Validating the P2 Engine

*Before building, we must ensure the tenant "knows" it has P2 powers.*

1. Go to **Identity** > **Overview**.
2. Verify that under **Licenses**, it explicitly says **Microsoft Entra ID P2**.
3. *Mac/2026 Fix:* If you just activated it, the "Dynamic User" button might still be grey. If so, sign out of the portal and sign back in to refresh your admin token.

### [ ] Phase 2: Building the Dynamic Infrastructure

1. Go to **Groups** > **All groups** > **+ New group**.
2. **Group type:** `Security`.
3. **Group name:** `Dynamic-Engineers-Group`.
4. **Membership type:** Change from "Assigned" to **Dynamic User**.
5. **Entra roles can be assigned to the group:** Select **No** (Dynamic groups cannot hold direct Entra roles).

### [ ] Phase 3: Writing the "Identity Logic" (Rule Builder)

*Instead of a Graph API query, we write a persistent rule that Entra monitors 24/7.*

1. Click **Add dynamic query**.
2. In the **Rule Builder**, set the following:
* **Property:** `jobTitle`
* **Operator:** `Equals`
* **Value:** `Cloud Engineer`


3. Click **Save** at the top.
4. Click **Create**.

### [ ] Phase 4: Triggering the "Automation Loop"

*To test this, we need to give a user the correct attribute.*

1. Go to **Identity** > **Users** > **All users**.
2. Select `lab-user-01`.
3. Click **Edit properties**.
4. Scroll to **Job Information** and set the **Job title** to: `Cloud Engineer`.
5. Click **Save**.

### [ ] Phase 5: Monitoring the Membership Processing

*In 2026, dynamic groups are not instant. They run on a processing cycle.*

1. Go back to **Groups** > **Dynamic-Engineers-Group**.
2. On the **Overview** page, look for **Dynamic group processing status**.
3. Wait until it says **Succeeded**.
4. Click **Members** on the left. `lab-user-01` should now appear automatically.

---

## 💬 Lab 2 Discussion History (P2 Automation Questions)

1. **What happens if I change a user's Job Title to 'Manager'?**
* **Answer:** Entra will automatically detect the change during the next processing cycle and **remove** them from the group. This is the "Self-Cleaning" nature of P2.


2. **Why can't I manually add a member to this group now?**
* **Answer:** Once a group is set to **Dynamic**, the "Add Members" button is disabled. The "Rule" is the only authority. This prevents "Permission Creep" where people stay in groups they no longer belong in.


3. **What is the "Processing Status" I see in the 2026 portal?**
* **Answer:** It tells you if the engine is currently scanning your directory. If it says "Paused," it usually means there is a syntax error in your rule.


4. **Can I use the Graph API to edit this rule?**
* **Answer:** Yes! Even with P2, you can use Graph to update the `membershipRule` property, but the Portal's **Rule Builder** is now safer because it validates your syntax before you save.



---

**Now that Lab 2 is fully upgraded to the P2 standard, your environment is ready for advanced security. Would you like to move to Lab 5: Conditional Access?**

**Modern 2026 Entra ID Workflow: Active**

Since you now have the **P2 License**, Lab 3 changes significantly. We are moving away from "Security Defaults" (which is a blunt tool) and moving toward **Dynamic Groups** that actually work automatically. You no longer have to "pretend" with validation—the system will now do the hiring and firing for you.

---

## 🛠 Lab 3: Identity Security & Dynamic Logic (P2 Edition)

### [ ] Phase 1: Disable Security Defaults (MANDATORY for P2)

*Security Defaults is for the Free tier. Because you now have P2, keeping this enabled will block you from creating the custom Conditional Access rules we need for the Payroll Portal in Lab 5.*

1. Path: **Identity** > **Overview** > **Properties**.
2. Action: Click **Manage security defaults**.
3. Toggle: Set to **Disabled**.
4. Reason: Select **"My organization is using Conditional Access"** and click **Save**.

### [ ] Phase 2: Building TRUE Dynamic Logic (Lab3-Sales-Group)

*Now that your P2 license is active, the "Create" button is no longer greyed out. We are building a group that automatically recruits any salesperson from Chicago.*

1. Navigate: **Groups** > **All groups** > **+ New group**.
2. **Basic Settings:**
* **Group type:** Security.
* **Group name:** `Lab3-Sales-Dynamic`.
* **Membership type:** Select **Dynamic User**.


3. **The Dynamic Query:** Click **Add dynamic query**.
4. **The Rule Builder (2026 Method):**
* Line 1: **Property:** `department` | **Operator:** `Equals` | **Value:** `Sales`.
* Click **+ Add expression**.
* Line 2: **And/Or:** `And` | **Property:** `city` | **Operator:** `Equals` | **Value:** `Chicago`.


5. **Click Save** and then click **Create**. The group is now "live" and scanning your directory.

### [ ] Phase 3: Formatting and Attribute Injection

*To make the automation work, our users must have the correct "metadata" (Attributes).*

1. Navigate: **Users** > **All users** > **+ New user**.
2. **Formatting Rule:**
* **UPN:** `chicago.sales@yourdomain.onmicrosoft.com` (No spaces allowed).
* **Display Name:** `Chicago Sales Rep`.


3. **The Injection (Properties):**
* Scroll to **Job Information**.
* **Department:** `Sales`.
* **City:** `Chicago`.


4. Click **Review + create** > **Create**.

### [ ] Phase 4: Verification (The Automation Proof)

*Instead of manually adding users, we watch the Entra Engine do the work.*

1. **Wait for Processing:** Go to **Groups** > `Lab3-Sales-Dynamic`.
2. **Overview Tab:** Check the **Dynamic group processing status**. In the 2026 UI, this usually takes 1–3 minutes.
3. **The Result:** Click **Members**. If your logic was correct and your user's attributes match, the `Chicago Sales Rep` will appear here automatically with **no manual intervention**.

---

## 💬 Lab 3 Discussion History (P2 Logic Questions)

1. **Why did we disable Security Defaults?**
* **Answer:** Security Defaults is "All or Nothing." P2 allows us to be surgical. We can demand MFA for the Payroll app but not for the company menu. You can't have both active at once.


2. **What is the difference between "Validate" and "Create"?**
* **Answer:** In the Free tier, you could only "Validate" (test the theory). In P2, "Create" actually starts a background service that monitors your users 24/7.


3. **What happens if the Sales Rep moves to New York?**
* **Answer:** As soon as you update their **City** attribute to `New York`, the P2 engine will automatically **evict** them from the Chicago group within minutes.


4. **Why use the "Rule Builder" instead of typing the syntax manually?**
* **Answer:** The 2026 Rule Builder prevents syntax errors (like the minus sign `−` vs the hyphen `-`) that often cause dynamic rules to fail on Mac keyboards.



---

**Lab 3 is now fully updated for your P2 environment! You have a self-managing Sales group. Are you ready to head back to our current progress and start Lab 5: Conditional Access?**

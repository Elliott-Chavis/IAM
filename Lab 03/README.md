Lab 3: Identity Security & Dynamic Logic
Phase 1: Enable Tenant-Wide Protection (Security Defaults)

Since you don't have P1/P2 licenses for custom Conditional Access, we use Security Defaults to enforce MFA for everyone.

Navigate: Sign in to the Microsoft Entra admin center.

Path: Go to Identity > Overview.

Properties: Click the Properties tab in the main window (next to "Overview").

Security Defaults: Scroll to the bottom and click Manage security defaults.

Action: Set the toggle to Enabled and click Save.

Troubleshooting: If you ever want to create custom policies in the future, you must come back here and disable this first.

Phase 2: Building "Dynamic" Logic (The Logic Drill)

You created two groups: Dynamic Engineers and Lab 3 Sales. Even though the Free Tier kept them as "Assigned," here is how you correctly configured the logic.

Navigate: Go to Groups > All groups > + New group.

Basic Settings:

Group type: Security.

Group name: Lab3-Sales-Dynamic.

Membership type: Select Dynamic User.

The Dynamic Query: Click Add dynamic query.

In the Rule syntax box (click "Edit" to type manually), enter:

(user.department−eq"Sales")−and(user.city−eq"Chicago")
The Validation Step (Crucial for Free Tier): * Since you cannot click Create on a Dynamic Group without a P1/P2 license, click the Validate Rules (Preview) tab.

Click + Add users and select your test user.

Green Checkmark: If you see a green check, your logic is perfect.

The Edit: Because the "Create" button was greyed out for Dynamic User, you switched the Membership Type back to Assigned and clicked Create.

Phase 3: Correcting User Creation (Formatting)

When you manually added users to test your environment, we found that the User Principal Name (UPN) has strict rules.

Navigate: Go to Users > All users > + New user.

Formatting Rule: * Wrong: test engineer@yourdomain.com (Spaces are not allowed in UPNs).

Right: test.engineer@yourdomain.com (Use dots or dashes).

Display Name: You can freely use spaces here (e.g., Test Engineer).

Job Info: To make your users "fit" your rules, click Properties during creation and set Department to Sales and City to Chicago.

Phase 4: Verification (The Final Proof)

To confirm Lab 3 is finished, you performed these two checks:

Test	Action	Success Criteria
MFA Test	Login via Incognito Window.	User is prompted for "More information required."
Logic Test	Check the Members tab of your group.	If membership is "Assigned," you manually add the user to prove they belong.

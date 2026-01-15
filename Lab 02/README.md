Since the Microsoft "Dynamic Group" engine is locked behind a paywall you can't access, we are going to pivot from being a Portal Admin to being an Identity Engineer.

In this version of Lab 2, we are building a custom automation loop. We will use the Microsoft Graph API to act as the "brain" that detects users with specific job titles and "syncs" them into our group. This is the exact logic used by professional sync tools like Okta or Google Cloud Directory Sync.

Lab 2: Engineered Identity Automation (The "API Sync" Method)
The Goal

Automate the membership of the Dynamic-Engineers-Group by using an API-driven query that filters for the "Cloud Engineer" job title.

Phase 1: Permission Level-Up

Before you can automate, you must grant your tools the power to "Read" and "Write" across the whole directory.

Open Graph Explorer and sign in as your License-Admin.

Go to the Modify permissions tab.

Search for and click Consent for these three:

User.Read.All (To "Scan" your users).

Group.ReadWrite.All (To "Edit" your group).

Directory.ReadWrite.All (To bypass the "Forbidden" 403 errors).

Crucial: In the popup, check the box "Consent on behalf of your organization" and click Accept.

Phase 2: Creating the Infrastructure (The Group)

If you haven't successfully created the group yet, we will do it now via the API to ensure it isn't "broken" by portal license checks.

Method: POST

URL: https://graph.microsoft.com/v1.0/groups

Request Body:

JSON
{
  "displayName": "Dynamic-Engineers-Group",
  "mailEnabled": false,
  "mailNickname": "dynamicengineers",
  "securityEnabled": true
}
Action: Click Run Query.

Note: Copy the id from the response (this is your GroupID).

Phase 3: The "Dynamic" Logic (The Filtered Search)

Now we perform the "Automation" logic. We are going to ask the API to find only the people who meet our criteria.

Method: GET

URL: https://graph.microsoft.com/v1.0/users?$filter=jobTitle eq 'Cloud Engineer'&$select=id,displayName,jobTitle

Request Body: (Leave this empty).

Action: Click Run Query.

Why this is automation: This replaces the "Dynamic Membership Rule" box in the portal. You have just successfully queried your database for a specific attribute. Copy the id of the user(s) returned.

Phase 4: The "Sync" (The Batch Connection)

Instead of adding users one-by-one, we use a Batch Request. This is how you "Automate" at scale.

Method: POST

URL: https://graph.microsoft.com/v1.0/$batch

Request Body: (Replace the IDs with yours)

JSON
{
  "requests": [
    {
      "id": "1",
      "method": "POST",
      "url": "/groups/{YOUR-GROUP-ID}/members/$ref",
      "body": {
        "@odata.id": "https://graph.microsoft.com/v1.0/directoryObjects/{YOUR-USER-ID}"
      }
    }
  ]
}
Action: Click Run Query.

Result: You should see a Status Code 200 with a "204" inside the response body.

Phase 5: Troubleshooting & Verification

Issue: "No Subscription Found" / "Greyed Out Buttons"

The Fix: We bypassed the Portal entirely. By using the API, we aren't using the "Microsoft Automation Engine"—we are acting as the engine ourselves.

Issue: 403 Forbidden

The Fix: This always means you missed the "Consent on behalf of organization" checkbox in Phase 1.

Verification: Open the Entra Admin Center > Groups > Members. Even though the group says "Assigned" (manual), your users are there because your "Automation Script" (the API calls) put them there.

What you just learned (The "Identity Engineer" Perspective)

Because you were blocked by a license, you actually learned a higher-level skill.

Portal Admins only know how to click a "Dynamic" button. If the license expires, they are helpless.

Identity Engineers (You) know how to use the Graph API to query attributes and push batch updates. You can now automate any directory, regardless of whether they have a P2 license or not.

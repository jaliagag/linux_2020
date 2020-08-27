# India Unix KT

[Session 1](https://web.microsoftstream.com/video/24f2f96d-b577-4143-8237-9f45771612c3)
[Session 1.5](https://web.microsoftstream.com/video/7a197d4e-ee38-436b-87f1-277332fe20fd)

Access to SNOW:

- enable `tabbed form` on the System Settings (gear icon) > **Forms**. 
- Set time zone to **America/Chicago** under your profile (your picture); Date format YYYY.MM.DD

Application bucket: look for **Change**.

## Create New (change)

Three change categories:

1. Normal: have to be scheduled 3 and 1/2 business days before the actual implementation. The tool will always allow you to create the change, but the process states that it should be created 3.5 days before implementation. It's used for Tier 4. Tier 2 patching. Regular change window from 23:00 to 05:00 CST. We need _approvals_ before doing them. Techncal, Business and CAB approvals.
2. Standard: tier 2 non-prod servers; also for hardware changes for tier 2, decommission of tier 2 servers (you can find the tier of the server under the `customer` tab). There is no review phase for standard changes. Regular schedule goes from 07:00 to 17:00 CST
3. Emergency: If we don't have 3.5 days and we have approval from a CSR/MD, then we create an Emergency change; for approvals you need to provide a P1 or P2 ticket to the CSR and they will provide the approval. Those approvals need to be attached on the same change.

### Creating a Standard change

There is no review for standard changes. Schedule: from 7AM to 5PM CST for non-production servers. For

1. Import template:
   1. click hamburguer icon > Templates > Apply Template > search for **AASM STD**
   2. Select whatever applies:
      1. AASM STD NonProd Software
      2. AASM STD NonProd Hardware
      3. AASM STD MLOS Microsoft Patching --> this would be for a _Normal Change_
2. Provide Assignment Group: **Server Unix - AASM**
3. Provide Configuration Item/Server name (if there are multiple, FIRST we have to save the change, with only one server; go to step 11 after completing the rest of the steps)
4. Company: **American Airlines Group Inc.**
5. Select Urgency and Priority (regularly 3 or 4); Riesk **None**
6. Short description: Typically, follow this format `server name | email subject line for reference | SR# for reference | Title of work`
7. Go to the Schedule tab and input Planned start date and Planned end date
8. Add the change plan; at the top, you'll see a clip, "Manage Attachments"; add the plan for the Standard Change being created (the planning tab is greyed out for Standard Changes, that's why we have to attach the plan; in _Normal Changes_ we have to input the plan information on the Panning tab).
9. Hit the "Outside maintenance schedule" in case the change happens outside the regular change window for the server.
10. Hit Save - please, make sure all the information is correct; we _CANNOT_ go back to make modificationafter we set these fields.
11. If there are multiple servers being affected by this Standard Change, at the bottom, go to the Affected CIs tab and add as many as necessary
12. After hitting Save, the Change will move to the _Review_ phase
13. Add the name of the person performing the change
14. Check for Conflicts with schedule. Go to the top of the top of the page, hit "Conflict Calendar"; that will display the "calendar" for the server/s selected, in case any other changes are happening during the same timeframe. (There is a bug saying that tehre is a conflict with the schedule); Also, please, go to the bottom of the page to the **Conflicts tab** and hit _Check Conflicts_ (the bug makes the system think that there is always a conflict).

### Working on a change

1. Change the state of the change to "In progress"
2. Do the planned work
3. Before the end time, please remember to change the status to "completed"; if you miss that dead line, the system will allow you to change the state 6 hours after the scheduled end time of the change.
4. Add close code and close notes

### Creating a Normal Change

1. Company
2. Assignment group
3. Category
4. CI name
   1. add more CIs under Affected CIs at the bottom of the page, in case more than one server is being affected.
5. Urgency 2
6. Priority 3
7. Short description - include SR numbers, something like SRQ2
8. Description: detailed description
9. Planning
   1. Justification - business justification. Format: `<Emp ID> <email_address@aa.com>`, for example: "AA Requester Employee ID:  @@00259824@@ AA Requester Email:SUNIL.SYAMALA@aa.com".
   2. Include Change, Implementation Backout and test plans (test plan 'tested as part of standard environment quarterly patching on stage and dev environments.', on which servers was it test _if it was tested_)
10. Got To Risk Assessment > Fill Out Risk Assessment. It depends on what is the change.
11. Hit Request Review at the top - it will trigger the review phase.
12. You can review the change again; make sure everything is ok
13. Hit Request Approval - it will trigger the approval phase - you wil _NOT_ be able to make modifications after the change goes to AA, to the reviewers, so make sure it's all complete.
    1. Technical Team: unix team
    2. App owners: approves on the AA side, using Cherwell
    3. CAB: change management team
15. Once all teams approve the change, we can start the change, at the scheduled time; when we do so, we have to _change the status to **in progress**_.
16. Once the change is complete, we have to
    1. Fill closure code and actual end time
    2. Fill the 3 tasks assigned to you (at the bottom, tab "Change tasks"):
       1. did you do the post-implementation plan?
       2. did you do the implementation plan?
       3. did you do the pre-implementation plan?
    3. Hit save
17. Close the change (tasks need to be marked as completed)

### Creating an Emergency Change

1. Attach approval email as attachment
2. Same fields as normal change
3. You can select any date that allows you to select

# ServiceNow Identity Tickets: Joiner, Mover, Leaver

Hands-on lab, Oct 2026.

On a help desk or IAM team, access changes start as tickets: someone new starts, someone changes roles, someone leaves. In this lab I ran all three tickets end to end in a ServiceNow developer instance. I took each ticket, did the actual change in Entra ID, logged what I did in work notes, and resolved it. The point is a clean paper trail from request to fix.

## What I built

- A ServiceNow Personal Developer Instance (Brazil release) with three incidents:
  - **INC0010001, joiner:** "New Hire Jane Smith needs an account and Finance-Users group access."
  - **INC0010003, mover:** "Test User moved teams - remove old group and add new group."
  - **INC0010004, leaver:** "Leaver Mike Lee - disable account and remove access."
- For each ticket I set the state to In Progress, posted a work note, did the change in Entra ID, posted another work note, filled in the resolution code and notes, and resolved it.
- Joiner: created Jane Smith in Entra ID, then created the Finance-Users security group with her as a member.
- Mover: added Test User to Finance-Users. Test User's old group, MFA-Test-Group, already had 0 members, because an earlier access review had removed them. I checked the group and noted that in the ticket.
- Leaver: disabled the account in Entra ID. Account status shows Disabled.
- **Note on names:** the leaver ticket names "Mike Lee". In my tenant, the lab account standing in for Mike Lee is **Leaver User**, and that is the account I disabled.

## What I learned

His own words (lightly cleaned up):

> I made a simulation of how I'll be answering tickets if I was on the job, through ServiceNow and Entra. I made examples for joiner, mover and leaver. I made the ticket for the joiner, answered it, updated it on what I was doing, and updated it when I fixed the issue. I did the same thing for the mover, when somebody is moving roles or might need access for something at a specific time: I made the ticket, put it in progress, updated it, did the work in Entra, updated the work notes, and resolved it in ServiceNow. And I did the same if someone was leaving: I made the ticket, updated the work notes, removed them in Entra and disabled their account, then went back into ServiceNow, updated the work notes on what I did, and resolved it.

*Interview line:*

> "I built a ServiceNow developer instance and simulated how I'd work identity tickets on the job. I made a joiner, a mover and a leaver ticket. For each one I set it In Progress, did the work in Entra ID (created the user and group access, moved someone's access, disabled the leaver's account), logged what I did in work notes, and resolved it with resolution notes. The activity log gives a full paper trail."

## Key screenshots

![](key/01-three-jml-tickets-created.png)
*Created joiner, mover and leaver tickets in my ServiceNow developer instance.*

![](key/02-joiner-ticket-in-progress-worknote.png)
*Set the joiner ticket to In Progress and logged a work note.*

![](key/03-entra-joiner-user-created.png)
*Created the new hire Jane Smith in Entra ID for the joiner ticket.*

![](key/04-joiner-added-to-finance-users.png)
*Added Jane Smith to the Finance-Users security group as requested.*

![](key/05-mover-added-to-finance-users.png)
*Mover ticket: added Test User to Finance-Users for the new role.*

![](key/06-leaver-account-disabled.png)
*Leaver ticket: Entra ID now shows the leaver account status Disabled.*

![](key/07-leaver-resolution-notes.png)
*Filled resolution code and notes before resolving the leaver ticket.*

![](key/08-all-three-tickets-resolved.png)
*All three joiner, mover and leaver tickets show Resolved in ServiceNow.*

## Environment

| Piece | What I used |
|---|---|
| Ticketing | ServiceNow Personal Developer Instance (Brazil release), Incident module |
| Identity | Microsoft Entra ID (lab tenant) |
| Accounts | Jane Smith (joiner), Test User (mover), Leaver User (stand-in for "Mike Lee", leaver) |
| Groups | Finance-Users (new), MFA-Test-Group (old group for the mover) |

## What broke / issues I fixed

- My first screenshot of Leaver User's Settings tab didn't clearly show whether "Account enabled" was unchecked. I went to the user's Overview page instead, where Account status reads **Disabled**, and used that as the proof.

## Gaps

- The mover's "remove old group" step had nothing left to remove. MFA-Test-Group was already empty from an earlier access review, so this lab shows the check, not the removal itself.
- The leaver ticket asked to "remove him from all groups". The proof shows the account disabled; it does not show a group-by-group removal.
- The tickets were raised as System Administrator, not as an HR caller or through a catalog request. That's fine for practice, but a real queue would look different.
- No automation: every step was done by hand in the portal.

<details><summary>Full proof (all screenshots)</summary>

![](full-proof/01-instance-ready.png)

![](full-proof/02-instance-home-signed-in.png)

![](full-proof/02b-new-incident-form-empty.png)

![](full-proof/03-incident1-joiner-form-filled.png)

![](full-proof/04-incident1-submitted-in-list.png)

![](full-proof/05-incident2-mover-INC0010003-in-list.png)

![](full-proof/05b-INC0010003-opened-activity-log.png)

![](full-proof/06a-incident3-leaver-INC0010004-form.png)

![](full-proof/07b-list-INC0010001-in-progress.png)

![](full-proof/08a-entra-new-user-jane-form.png)

![](full-proof/08-jane-smith-in-user-list.png)

![](full-proof/09a-new-group-finance-users-form.png)

![](full-proof/10a-INC0010001-worknote-posted.png)

![](full-proof/10b-INC0010001-resolution-filled.png)

![](full-proof/10-INC0010001-resolved.png)

![](full-proof/11a-INC0010003-in-progress-worknote.png)

![](full-proof/12-mfa-test-group-0-members.png)

![](full-proof/13a-INC0010003-worknote.png)

![](full-proof/13-INC0010003-resolved.png)

![](full-proof/14a-INC0010004-in-progress-worknote.png)

![](full-proof/14b-leaver-user-settings-unclear.png)

![](full-proof/15a-INC0010004-worknote-posted.png)

</details>

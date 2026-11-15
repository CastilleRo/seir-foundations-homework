# Week 5: Lesson 3, Jira Cloud Free (Notes)

Handle: Shibumi. Date: Nov 15, 2026. Plan: Jira Cloud Free.

## What I built

- My own Atlassian account and Jira Cloud Free site (the site URL is kept private and is not in this repo).
- A team-managed Kanban space named **Balerica AI Incident Management** with project key **BAI**.
- Statuses: To Do, In Progress, Done (plus the Backlog and Reports views covered in class).
- A manual test incident: **BAI-4**, type Task, summary `TEST — EC2 application error`, with the description from the lab.
- Config saved in a private note on my laptop (site URL, email, project key, test issue key, default issue type). Nothing secret is in this repo.

## Purpose of the lab

Slack tells a human that something happened. Jira keeps a record of it and its follow-up. In a later lab, `jira.py` will call the Jira Cloud REST API and create a ticket automatically when Balerica AI detects an error: detect, alert, ticket. This lab is the groundwork: a site, a project, its key, and one manual ticket to prove it works.

## Things that did not go as the lab expected

- **Project key:** Jira first gave the space the key `KAN`. I changed it to `BAI` under Space settings > Details. Jira warned that changing the key re-indexes the space; nothing external used it yet. The old key shows as a "previous space key". Lesson: verify the actual key, do not assume it.
- **Ticket numbers:** Jira adds sample tickets (BAI-1 to BAI-3) to every new space, so my first real ticket is BAI-4, not BAI-1. The sample statuses are only placeholders.
- **Access:** the space was created as Open, meaning anyone on my site can see it. I changed it to Private, as in class.
- **Privacy:** my account showed my real name. I changed the Full name and Public name to Shibumi, and confirmed my email is visible to "Only you and admins".
- **No API token:** the lab says not to create one yet. When it is needed, use the plain "Create API token" option (not "with scopes"), store it only in `.env`, and record its expiry date.

## Class notes (Nov 10 and Nov 14)

- Hierarchy: Epic (big problem) > Story > Task > Subtask. Class example epic: GTA 6 downtime, with stories for script creation, monitoring, longer SLA and agentic AI.
- Story points: 1 point is about 1 day of work. Typical sprint load is 7 to 8 points. Turn on Estimation under Space settings > Features.
- Jira is where you record work, blockers and progress so others can see it without asking.

## Evidence files

- `jira-01-board-bai-incident.png`: list view with the space name and BAI-4
- `jira-02-test-incident-bai4.png`: BAI-4 opened, showing summary, description and key
- `jira-03-space-key-bai.png`: Space settings > Details showing key BAI

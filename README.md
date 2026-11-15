# seir-foundations-homework

Homework for SEIR Foundations (Class 8).

## Contents

- [Lab 0: basics](module1/lab0_basics)
- [Lab 0.5: basics, continued](module1/lab0.5_basics_contd)
- [Balerica Legacy Bank install (runbook steps 0-9)](#balerica-legacy-bank-install-runbook-steps-0-9), runs 1-5 below
- [Lesson 2: Slack alerts (Week 4)](#lesson-2-slack-alerts-week-4)
- [Lesson 3: Jira Cloud Free (Week 5)](#lesson-3-jira-cloud-free-week-5)

## Balerica Legacy Bank install (runbook steps 0-9)

Completed **5 runs**: 4 standard runs plus 1 run that includes the **Step 8 Student Challenge (Amazon Bedrock)**.
Each run was launched from the launch template `Shibumi_seir-lab0-template` (versions v2 to v6), followed the runbook, collected a screenshot evidence set, and was terminated afterward.

| Run | Launch template | Screenshots | Notes |
|---|---|---|---|
| 1 | v2 | [module1/run1-template-v2](module1/run1-template-v2) | [run1-notes.md](run1-notes.md) |
| 2 | v3 | [module1/run2-template-v3](module1/run2-template-v3) | [run2-notes.md](run2-notes.md) |
| 3 | v4 | [module1/run3-template-v4](module1/run3-template-v4) | [run3-notes.md](run3-notes.md) |
| 4 | v5 | [module1/run4-template-v5](module1/run4-template-v5) | [run4-notes.md](run4-notes.md) |
| 5 (Bedrock challenge) | v6 | [module1/run5-template-v6-bedrock](module1/run5-template-v6-bedrock) | [run5-notes.md](run5-notes.md) |

## Bedrock Student Challenge (Step 8): where to find it

The challenge is in **run 5**: [module1/run5-template-v6-bedrock](module1/run5-template-v6-bedrock), with the write-up in [run5-notes.md](run5-notes.md).

Goal: make `/ask` answer from Amazon Bedrock instead of the offline knowledge base.

- Created an IAM role with `bedrock:InvokeModel` and attached it to the instance.
- Set `AWS_REGION` and `BEDROCK_MODEL_ID` before starting `uvicorn`.
- `/ask` stayed offline. Direct `invoke-model` tests showed Claude Sonnet 5.5 was not available to the account, while Sonnet 4.6 worked.
- Calling the app's own function revealed the hidden error: missing AWS Marketplace permissions for the first-time model subscription.
- Added those permissions, waited, and `/ask` returned `"source":"amazon-bedrock"`.

Key evidence screenshots in the run 5 folder:
- `run5-05a-ask-still-offline`: before
- `run5-05c-bedrock-marketplace-error`: the diagnosis
- `run5-05e-role-policy-marketplace`: the fix
- `run5-05-ask-bedrock`: the result

## Lesson 2: Slack alerts (Week 4)

Connected the Balerica bank EC2 instance to my own Slack workspace so Python scripts send alerts to `#balerica-alerts` through an Incoming Webhook. Completed the seven homework scripts (hw1 to hw7) and the four experiments.

All files are in [module1/lesson2_slack_hw](module1/lesson2_slack_hw):

- [week4-notes.md](module1/lesson2_slack_hw/week4-notes.md): setup, the answer to each script's "In your notes" question, and the experiments (prediction vs result)
- `slack-01-test-alert.png`: first alert from `python slack.py --test`
- `slack-02-hw-alerts.png`: Slack channel showing alerts from five different homework scripts
- `slack-03-hw7-terminal.png`: terminal with the ID line and the morning report

Setup notes: launched a fresh instance from template v6 as `ec2-user`, installed the bank, and saved a clean AMI (`Shibumi-bank-no-slack-Nov09`) before adding any Slack configuration.

## Lesson 3: Jira Cloud Free (Week 5)

Created my own Jira Cloud Free site and a team-managed Kanban space, **Balerica AI Incident Management** (key `BAI`), then a manual test incident, `BAI-4`: `TEST — EC2 application error`. A later lab will have `jira.py` create tickets like this automatically from Balerica AI errors.

All files are in [module1/lesson3_jira_hw](module1/lesson3_jira_hw):

- [week5-notes.md](module1/lesson3_jira_hw/week5-notes.md): setup, what did not go as expected (key `KAN` changed to `BAI`, sample tickets, access set to Private), and class notes
- `jira-01-board-bai-incident.png`: list view with the space and BAI-4
- `jira-02-test-incident-bai4.png`: BAI-4 opened
- `jira-03-space-key-bai.png`: space settings showing key BAI

No API token was created, as the lab instructs.

## Privacy

AWS account identifiers and user names are redacted in all screenshots. Slack workspace URLs are covered in the Week 4 screenshots, and the Jira site URL and email are not shown in the Week 5 screenshots. No keys, credentials, `.env` files or webhook URLs are included. YOU AIN'T GETTIN' THEM! :)

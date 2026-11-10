# Week 4: Lesson 2, Slack Alerts (Notes)

Handle: Shibumi. Date: Nov 9-10, 2026. Region: us-east-1. Logged in as `ec2-user`.

## What I built

- A private Slack workspace with a `#balerica-alerts` channel and a Slack app called `Balerica AI` with an Incoming Webhook (the webhook URL stays private in `.env` on the instance and is never committed).
- Launched a fresh instance from template v6, installed the Balerica bank from the class repo, and saved a clean AMI before touching Slack: `Shibumi-bank-no-slack-Nov09`.
- Copied `slack.py` and the seven homework scripts into `/opt/balerica-bank`, set my workspace URL, and ran `python slack.py --test`, which printed `SUCCESS: Chewbacca approves!` and showed the alert in Slack.
- Protected the webhook: `.env` is `chmod 600` and listed in `.gitignore`.

## Lab questions

**Difference between `SLACK_WORKSPACE_URL` and `SLACK_WEBHOOK_URL`:** The workspace URL (in `slack.py`) is only a label and a check; it is not secret and does not route messages. The webhook URL (in `.env`) is the private address Slack gives the app. Anyone who has it can post to my channel, so it is a secret. Changing the workspace URL does not change where alerts go.

**A question I asked Claude and how I checked it:** I asked which of the four alerts would arrive if the threshold was CRITICAL. I checked the answer myself by changing `.env`, rerunning `hw2_severity_tour.py`, and looking at the terminal and Slack. Only CRITICAL arrived.

## Script notes (In your notes:)

**hw1_hello_slack.py:** Set `MY_NAME = "Shibumi"`. The script printed `Delivered!` and the alert appeared in Slack with Incident HW-001.

**hw2_severity_tour.py: which severities arrived, and why?** All four (INFO, WARNING, ERROR, CRITICAL) arrived because `SLACK_ALERT_SEVERITY=INFO` is the lowest threshold, so nothing is filtered out.

**hw3_server_time.py: how many hours apart are server time and my wall clock?** 5 hours. The server runs on UTC (16:36 UTC); my clock was on EST (11:36), which is UTC-5.

**hw4_disk_watch.py: why is a quiet INFO good design, not a failure?** Disk was 25.4% used, so the script chose INFO. A quiet INFO means the check ran and everything is healthy. If every healthy check paged a person, people would start ignoring alerts, so a system that stays quiet when nothing is wrong is working.

**hw5_load_check.py: what would make this number spike on the Balerica bank?** Load was 0.00 on 2 CPUs. It would spike with heavy traffic (the SWIFT traffic generator or many payment/`/ask` requests at once), bulk COBOL batch jobs, slow calls waiting on Bedrock, or a stuck process in a loop.

**hw6_incident_drill.py: which fake incidents deserve to wake a human at 3 AM?** I ran it five times and drew:

| Incident | Severity | Message |
|---|---|---|
| DRILL-5239 | INFO | Nightly ledger backup completed successfully |
| DRILL-4923 | INFO | Nightly ledger backup completed successfully |
| DRILL-4710 | INFO | Nightly ledger backup completed successfully |
| DRILL-7457 | WARNING | COBOL batch job BATCH-EOD running 12 minutes longer than usual |
| DRILL-1262 | ERROR | payment_post returned code 8: business rejection rate above 5% |

Only the ERROR (payments being rejected, customers affected) deserves a 3 AM call, and only if it keeps rising. INFO is a record, and the WARNING can wait until morning.

**hw7_morning_report.py:** Sent a full morning report (time, host, Python version, disk, load, status) to Slack. Terminal evidence with the ID line is in `slack-03-hw7-terminal.png`.

## Experiments

**1. Threshold = CRITICAL, rerun hw2.**
- Prediction: only CRITICAL arrives, because INFO, WARNING and ERROR (ranks 0, 1, 2) are below the threshold rank of 3.
- Result: only CRITICAL was delivered. The terminal said `skipped by your threshold` for the other three.
- Lesson: the threshold is the minimum severity allowed through.

**2. `SLACK_ALERTS_ENABLED=false`, run hw1.**
- Prediction: no message.
- Result: nothing reached Slack; the script printed `Skipped. Check .env...`. I set the threshold back to INFO at the same time so only the on/off switch could block it.
- Lesson: `SLACK_ALERTS_ENABLED` is a master off switch that works before the severity check.

**3. Lower the hw4 WARNING cutoff from 75 to 10.**
- Prediction (my honest first guess): INFO and no alert. I was wrong: disk was 25.4%, which is above 10.
- Result: severity WARNING, delivered to Slack.
- Lesson: the cutoffs in the code decide what counts as worth alerting on.

**4. Restore.** Put the cutoff back to 75 and confirmed `.env` has `SLACK_ALERTS_ENABLED=true` and `SLACK_ALERT_SEVERITY=INFO`.

## What I learned

- Alerts are only useful if they are filtered: quiet when healthy, loud when something needs a human.
- The webhook URL is a secret and must never go in GitHub, screenshots or chat.
- Launching from a custom AMI can log you in as `root`; check `whoami` and use `ec2-user`.
- Verify before you trust: a success message in the terminal is not proof until the alert shows in Slack.

## Evidence files

- `slack-01-test-alert.png`: first test alert from `slack.py --test`
- `slack-02-hw-alerts.png`: Slack channel showing alerts from five different scripts
- `slack-03-hw7-terminal.png`: terminal with ID line and the morning report

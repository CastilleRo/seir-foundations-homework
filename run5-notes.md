# Run 5: Step 8 Student Challenge (Amazon Bedrock)

Goal: make `/ask` answer from Amazon Bedrock instead of the offline knowledge base.

- Created IAM role `BalericaLegacyBankEC2Role` with `bedrock:InvokeModel` and attached it to the instance (Modify IAM role). Template v6 did not carry the instance profile; a v7 fix is planned.
- Set `AWS_REGION=us-east-1` and `BEDROCK_MODEL_ID` before starting `uvicorn`.
- `/ask` stayed on `offline-knowledge-base`. Direct `aws bedrock-runtime invoke-model` tests showed Claude Sonnet 5.5 was not available for the account, while Sonnet 4.6 (`global.anthropic.claude-sonnet-4-6`) worked.
- Calling the app's own `bedrock_answer()` function revealed the hidden error: `AccessDeniedException` for missing AWS Marketplace actions (`aws-marketplace:ViewSubscriptions`, `aws-marketplace:Subscribe`).
- Fix: added those two actions to the role's policy, waited about five minutes, and `/ask` then returned `"source":"amazon-bedrock"`.
- Lesson: the app's fallback hides the real error, so reproduce the call outside the app to read it.

Evidence: `run5-00` to `run5-07`, including `05a` (still offline), `05c` (Marketplace error), `05e` (policy fix), and `05` (Bedrock answer).

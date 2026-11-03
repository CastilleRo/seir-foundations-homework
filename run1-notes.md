# Run 1: launch template v2 (t3.small)

First full install of the Balerica Legacy Bank, following runbook steps 0-9.

- Created the security group `BankofShibumi_sg` (ports 22, 80, 8000) and launch template v2.
- Launched the instance, cloned the repo, and ran `install.sh`.
- Verified the COBOL core: account lookup, a posted payment, and a rejected 5,000,000 payment.
- Started FastAPI/uvicorn, ran the SWIFT traffic generator, and used the `/docs` page.
- `/ask` answered from the offline knowledge base.
- Terminated the instance afterward.

This run has the fullest screenshot set (20) because it also covers the setup.

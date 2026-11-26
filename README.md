# solar-sense-AI-
Security review, pre-launch checklist, and incident response plan for the Solar Sense AI platform deployed on Render.
Solar Sense MVP: Security Review and Pre-Launch Checklist

A security checklist I authored for the Solar Sense MVP, a cloud-hosted web application deployed on Render. It was produced for my capstone project in the Women Techsters Fellowship (Cybersecurity Track), working directly with the team's DevOps engineer.

Role: Cybersecurity Analyst (capstone team)
Platform: Render
Purpose: Every item below must reach PASS before the production launch.

1. SSL/TLS Certificate Integrity
[ ] Verify that the Render dashboard displays a Verified status for all custom domains.
[ ] Confirm that Render managed TLS is active and successfully provisioned.
[ ] Ensure automatic HTTPS redirection is enabled to force all HTTP traffic to port 443.
2. Server Hardening and Network Security
[ ] Audit service settings to ensure all public ports are closed, with exceptions only for ports 80 and 443.
[ ] Restrict cipher suites to support only TLS 1.2 and TLS 1.3.
[ ] Implement HTTP Strict Transport Security (HSTS) headers at the application level.
[ ] Configure a health check path to enable Render's automatic restarts for unresponsive instances.
[ ] Enable Render Protected Environments to prevent accidental service deletion or unauthorized configuration overrides.
3. Monitoring, Logging, and Alerts
[ ] Enable critical alerts for service downtime, unhealthy states, repeated restarts, and resource exhaustion (CPU/memory).
[ ] Integrate Render notifications with designated Slack channels for real-time response.
[ ] Centralize log delivery using stdout/stderr. Retain logs for a minimum of 14 days.
[ ] Verify that logs capture sufficient application, access, and security events for incident investigation.
[ ] Restrict log access to the DevOps Engineer and Cybersecurity Analyst with read-only permissions.
4. Backup Systems
[ ] Enable automatic backups for Render managed databases and verify the backup schedule.
[ ] Confirm backups are encrypted at rest and access is restricted to authorized personnel.
[ ] Document and test the restoration process to ensure data integrity.
5. Environment and Secret Management
[ ] Migrate all credentials (database strings, API keys, JWT secrets) from GitHub to Render Secret Groups.
[ ] Ensure all secrets are masked within the Render UI and deployment logs.
[ ] Maintain strict isolation between production and non-production environments.
[ ] Prohibit shared credentials or storage volumes between staging and production.
6. DDoS and Resource Protection
[ ] Apply rate limiting to public API endpoints based on IP address or user session.
[ ] Implement stringent rate limits specifically for AI inference endpoints to prevent resource abuse.
[ ] Define CPU and memory limits per service so requests are queued or blocked when thresholds are met.
7. Deployment Security
[ ] Conduct pre-deployment reviews and automated secret scanning before merging code.
[ ] Enable dependency vulnerability scanning via CI tools. Patch all critical vulnerabilities before deployment.
[ ] Verify that the rollback procedure is functional and can be executed in under five minutes.
[ ] Establish controlled deployment windows and document the protocol for emergency hotfixes.
8. Access Control
[ ] Enforce MFA for the Render workspace and the linked GitHub organization.
[ ] Restrict production environment access to essential personnel only (maximum of 5 users).
[ ] Disable root login and mandate key-based authentication via the Render CLI or dashboard for all team members.

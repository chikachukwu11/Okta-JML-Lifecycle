# IAM Lifecycle Runbook: Meridian Trust Bank (Okta)
<h2>Desisgn Principles</h2>

  - <b>Group-Based Assignment Only:</b> Apps are assigned to groups, never to individual people. Strict group-to-app wiring prevents privilege creep and ensures clean automation.
  - <b>Attribute-Driven Membership:</b> Group memberships are automatically assigned based on identity attributes (e.g., Departments) instead of being individually assigned by admins, speeding up the joiner, mover, leaver process.
  - <b>Least-Privilege Admin:</b> Administrative access is restricted based on functional roles. Full configuration access is limited to only authorized super admins. Helpdesk admins are only given the specific access required to manage users and credentials, without full configuration rights.

<h2>Joiner</h2>

  - <b>Trigger:</b> A new employee is hired. ( Simulated by manual creation in Okta) (Typically done by HR Import or SCIM feed, ideally scheduled to activate on the start date)
  - <b>Operator:</b> IAM Administrator
  - <b>Required Attributes:</b> First name, Last name, Username/Email, and Department (e.g., "Lending" or "Payments")
  - <b>Automated Actions:</b> The new user is assigned birthright access (All-Staff). Then the new user is automatically assigned to a role group and provisioned with relevant application access based on the department attribute entered when the user was created (e.g., "Lending" or "Payments").
  - <b>Evidence Produced:</b>

<h2>Mover</h2>

  - <b>Trigger:</b> 
  - <b>Operator:</b> IAM Administrator
  - <b>Attribute Change:</b>
  - <b>Automated Actions:</b> 
  - <b>Evidence Produced:</b>

<h2>Leaver</h2>

  - <b>Trigger:</b> An employee resigns or is terminated from the organization.
  - <b>Operator:</b> IAM Administrator
  - <b>Attribute Change:</b> Account deactivation
  - <b>Automated Actions:</b> Group membership removal, MFA factors reset, OAuth access/refresh tokens revoked, API tokens revoked, AD account disabled, and password scrambled, if AD-integrated.
  - <b>Okta workflows extras (Not added into Lab):</b> Notify manager/IT, open a ServiceNow Ticket, delegate mailbox, transfer Drive files, reclaim licenses.
  - <b>Evidence Produced:</b> System logs capturing the deactivation event itself, group membership removal, app assignments removal, app entitlements removal, MFA factor resets, workflow execution history if Okta flows are used.

<h2>Authentication Policy</h2>

  - <b>MFA Enrollment:</b> Okta Verify App enrollment is marked as required in the enrollment policy. This makes MFA an enforced control rather than a user choice. Forcing enrollment at first sign-in eliminates any enrollment gaps among user accounts. Passwords are assumed compromised, MFA is the compensating control, so it has to cover 100% of accounts, and policy-level enforcement is the only way to prove that to an auditor. Also, NIST guidelines, CIS controls, and cyber insurance providers all expect and require mandatory MFA
  - <b>Password Policy:</b> Password requirements are hardened to require a minimum length of 12+ characters, requiring the use of uppercase and lowercase letters, numbers, and special symbols. There is also a common password blocklist check and account lockout after 10 failed attempts.
  - <b>Routine Expiry Disabled:</b> Routine password expiry is off deliberately and backed by NIST guidelines. Forced periodic password changes make security worse. Users respond with predictable increments that attackers model easily (Winter2025! to Spring2026!). Stolen credentials are used within hours or days; a 90- day or 120-day expiry never catches that. Rotation drives password reuse, sticky notes, and helpdesk reset tickets. There is no real risk reduction, but there is a real cost associated with it.

  <h2>Admin Model</h2>

  - <b>Super Administartors:</b> Super admin status is restricted to the primary IAM infrastructure accounts only.
  - <b>Helpdesk Administartors:</b> Help desk admins possess standard help desk admin authorizations. The role permissions are strictly limited to looking up users, unlocking accounts, and resetting passwords or authentication factors. The role has zero access to change security policies, modify applications, or adjust group rules.

<h2>Lab Shortcuts vs. Production</h2>

  - <b>Admin Set Passwords:</b> 
  - <b>Bookmark Apps:</b> 
  - <b>Fake Email Domain:</b>

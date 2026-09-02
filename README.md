# Okta JML Lifecycle Automation

I	built	an	automated	joiner-mover-leaver	identity	lifecycle	in	a	free	Okta org,	modeled	on	a	fictional	bank	(Meridian	Trust	Bank).	Access	is	never assigned	to	people:	apps	bind	to	groups,	group	rules	place	people	in	groups from	their	HR	attributes,	and	the	lifecycle	runs	itself.	

## Operations
- [Runbook](Runbook.md) 

## What does this demonstrate?
- Role-based	access	via	groups	and	group-bound	application	assignment
-	Attribute-driven	group	rules	(HR-driven	provisioning	pattern)
- Full	JML	lifecycle:	automated	provisioning,	mover	access	swap,	leaver deactivation	with	session	kill
-	MFA	enrollment	policy	and	hardened	password	policy
-	Least-privilege	delegated	administration
-	Audit	evidence	for	every	lifecycle	event	from	the	Okta	System	Log

## Create Okta Org
  - Step 1: Sign up and open the Admin console.
    - Go	to developer.okta.com/signup.	The	page	shows	two	products	side	by	side:	Auth0	Platform	and	Okta	Platform. Scroll down	to	the	section	headed	"Access	the	Okta	Integrator	Free	Plan"	and	click	" Sign	up	for free.	

<img src="images/IAM-1.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-2.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-5.png" height="80%" width="80%" alt="JML-Lifecycle"/>

## Build groups and apps
  - Step 2: Create role groups
    - Create four groups that mirror the fictional bank structure
<img src="images/IAM-6.png" height="80%" width="80%" alt="JML-Lifecycle"/>

  - Step 3: Add the applications
    - Add the three applications that stand in for the fictional bank's systems.
<img src="images/IAM-7.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-8.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-9.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-10.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-11.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-12.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-13.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-14.png" height="80%" width="80%" alt="JML-Lifecycle"/>

  - Step 4: Link the apps to the groups
    - Assign each app to groups, not people.
<img src="images/IAM-15.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-16.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-17.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-18.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-19.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-20.png" height="80%" width="80%" alt="JML-Lifecycle"/>

## Automate Everything: create rules
  - Step 5: Create rules
    - Create rules that place personnel into groups based on their roles so that group membership is automated.
    - Create a rule that places all active personnel into the All-Staff group.
<img src="images/IAM-21.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-22.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-23.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-24.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-25.png" height="80%" width="80%" alt="JML-Lifecycle"/>

## Run the lifecycle
  - Step 6: The joiner
    - Hire the first employee into the lending department.
    - Log in as the new employee and verify they have the correct app and group permissions.
<img src="images/IAM-26.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-27.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-28.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-29.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-30.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-31.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-32.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-51.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-52.png" height="80%" width="80%" alt="JML-Lifecycle"/>

  - Step 7: The mover
    - The new employee transfers from the lending department to the payments department.
<img src="images/IAM-33.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-34.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-35.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-53.png" height="80%" width="80%" alt="JML-Lifecycle"/>

  - Step 8: The leaver
    - After joining and transferring departments later on, the employee has decided to resign and pursue other opportunities.
    - Log in as the previous employee, and the login fails.
<img src="images/IAM-36.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-37.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-38.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-39.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-40.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-54.png" height="80%" width="80%" alt="JML-Lifecycle"/>

## Harden: MFA, password policy, least admin privilege
  - Step 9: Make multifactor authentication mandatory.
<img src="images/IAM-41.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-42.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-43.png" height="80%" width="80%" alt="JML-Lifecycle"/>

  - Step 10: Strengthen the password policy
    - Default password policy: minimum length 12+, does not contain part of username, requires uppercase, lowercase, number, special symbol; enable common password check; set lockout after 10 failed attempts.
<img src="images/IAM-44.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-45.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-46.png" height="80%" width="80%" alt="JML-Lifecycle"/>

  - Step 11: Delegate helpdesk admin
    - Create a new helpdesk employee with no department
    - Add an administrator, grant the helpdesk administrator role only
<img src="images/IAM-47.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-48.png" height="80%" width="80%" alt="JML-Lifecycle"/>
<img src="images/IAM-49.png" height="80%" width="80%" alt="JML-Lifecycle"/>


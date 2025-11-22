# sailpoint


Gatner: provides rankings for iam solutions

Pillars of iam


|identity management --> access rights management-->  authentication management                                   --> privileged access management
|                                               |
|                                               |
|					        |	
|	Iam for users(sailpont,)	        |  Iam for applications(ping identity,ota,microsoft)                 cyberark




identity and access governance architecture:


hr  system is the entry point or source for identity source


employee ---> hr system ---> inserted into iag solution--> identity will be provisioned --->  manager gives authorization ---> automatic roles will be assigned --> provisioning of identity and its access is performed in  centralized directory ( ex: active directory ) and this directory is interfaced with applications either on prem or cloud. Every time a user logs into application interface with this directory to check users authorization.
 



iam --> provide access
iag --> auditing and checking whether it complies with governance or not.



iag main end users:

standard user: access request in self service, access rights visualization
manager: access request for their team, access review for their team, access approval for their team, define access needed for their team.
assistant: access request in place of manager, access approval in place of manager
security: access review for critical assets, access approval for critical access
application owner: access review and approval for their application.
auditor: They need access to variety of information & reporting necessary to control  security and compliance of the company reg regulations.


A stakeholder is someone who cares about or is affected by what you’re doing



IAG main stakeholders:


iam team: iam functional & technical

security and compliance team: ciso,governance team, business continuity team

business team: hr, procurement, app owners,assistants,mamager

architects: iam, security, enterprise architects


identity management capabilities:


identity model: every identity is represented by attribute and it is mainly a digital copy of physical identity.

identity classification: classified into employees, providers, patners and we can assign specific roles to each identity types.


authoritative sources: hr systems and this associates with IG solution.


identity life cycle:  created -> change role --> deactivated --> deleted

unique identifier: for each identity this is necessary for compliance reasons.

identity certification: IAG need to perform identity certification & revocation especially for dormant identities that are not  being used.

Identity Certification = Reviewing and confirming that a user’s access is still valid and necessary.

Identity Model:

Identity: Who you are in the organization (your digital representation) and can be associated to none,one or more accounts.

Account: A resource tied to credentials and permissions that lets you log in to systems/services.

Access Rights: permissions you have (what you can do).

Attributes: Details about your identity—like name, email, department, job title, location, employee ID, etc.

ex:
 
employee : john 

accounts:

windows account: login,pwsd

GitHub account: login,pwsd

access rights: IT role, business role

attributes
first name,last name, mail,job title, status,dept..



identity iq  (on-prem solution of vendor - sailpoint



Lab SailPoint IIQ: Discovery of the identity Model:

SailPoint already installed, preconfigured


post login we can see 

identities tab:  where we can manage the identities, create, delete & modifying..

applications tab:   where we can manage the rights catalogue that will be assigned to users & essentially managing authorizations


Intelligence tab: where we can see the audit & reporting menu.

Setup: we can see this if user is admin



lets have a quick look on identity and its representation by navigating to 

identities --> identity warehouse- we can see lot of identities and also at top bottom we can see overall count of identities


 under entitlements tab we can see roles and entitlements

Entitlements = individual permissions
Roles = bundles of entitlements for a job function


Roles at the top that provides rights which are displayed at bottom

Under application accounts  we can see which accounts are associated with the identity

we can drag the drop down of any application account and we can see whether the account status, locked yes or no..


by default we will be seeing hr employees under application accounts of any identity as it is a source of identity data that will be synchronized with the IG solution.


Under User Rights menu we can see the  what platform-level rights that they have for IdentityIQ.


















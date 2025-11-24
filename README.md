# Sail Point
- Gatner: provides rankings for iam solutions

- Pillars of iam

```
identity management            access rights management                  authentication management   privileged access management
|                              |                                          |                            |
|                              |                                          |                            |
|					                         |	                                         |                            |
|                              |                                          |                            |              
Iam for users(sailpont)       Iam for applications.. sailpoint            ping identity,okta           cyberark
```



## identity and access governance architecture:


- hr  system is the entry point or source for identity source


- employee ---> hr system ---> inserted into iag solution--> identity will be provisioned --->  manager gives authorization ---> automatic roles will be assigned --> provisioning of identity and its access is performed in  centralized directory ( ex: active directory ) and this directory is interfaced with applications either on prem or cloud. Every time a user logs into application interface with this directory to check users authorization.
 
- iam --> provide access
- iag --> auditing and checking whether it complies with governance or not.



## iag main end users:

- **standard user**: access request in self service, access rights visualization
- **manager**: access request for their team, access review for their team, access approval for their team, define access needed for their team.
- **assistant**: access request in place of manager, access approval in place of manager
- **security**: access review for critical assets, access approval for critical access
- **application owner**: access review and approval for their application.
- **auditor**: They need access to variety of information & reporting necessary to control  security and compliance of the company reg regulations.


- A **stakeholder** is someone who cares about or is affected by what you’re doing



## IAG main stakeholders:


- **iam team**: iam functional & technical

- **security and compliance team**: ciso,governance team, business continuity team

- **business team**: hr, procurement, app owners,assistants,mamager

- **architects**: iam, security, enterprise architects

## identity management capabilities:

- **identity model**: every identity is represented by attribute and it is mainly a digital copy of physical identity.

- **identity classification**: classified into employees, providers, patners and we can assign specific roles to each identity types.


- **authoritative sources**: hr systems and this associates with IG solution.


- **identity life cycle**:  created -> change role --> deactivated --> deleted

- **unique identifier**: for each identity this is necessary for compliance reasons.

- **identity certification**: IAG need to perform identity certification & revocation especially for dormant identities that are not  being used.

- **Identity Certification** = Reviewing and confirming that a user’s access is still valid and necessary.

## Identity Model:

- **Identity**: Who you are in the organization (your digital representation) and can be associated to none,one or more accounts.

- **Account**: A resource tied to credentials and permissions that lets you log in to systems/services.

- **Access Rights**: permissions you have (what you can do).

- **Attributes**: Details about your identity—like name, email, department, job title, location, employee ID, etc.

### example:
 
- employee : john 

- accounts:

 - windows account: login,pwsd

 - GitHub account: login,pwsd

- access rights: IT role, business role

- attributes
 - first name,last name, mail,job title, status,dept..


- identity iq  (on-prem solution of vendor - sailpoint )

## Lab SailPoint IIQ: Discovery of the identity Model:

- SailPoint already installed, preconfigured


- post login we can see 

 - **identities tab**:  where we can manage the identities, create, delete & modifying..

 - **applications tab**:   where we can manage the rights catalogue that will be assigned to users & essentially managing authorizations


- **Intelligence tab**: where we can see the audit & reporting menu.

- **Setup**: we can see this if user is admin



- lets have a quick look on identity and its representation by navigating to 

- **identities --> identity warehouse**- we can see lot of identities and also at top bottom we can see overall count of identities


-  under **entitlements** tab we can see roles and entitlements

- Entitlements = individual permissions
- Roles = bundles of entitlements for a job function


- Roles at the top that provides rights which are displayed at bottom

- Under **application accounts**  we can see which accounts are associated with the identity

- we can drag the drop down of any application account and we can see whether the account status, locked yes or no..


- by default we will be seeing hr employees under application accounts of any identity as it is a source of identity data that will be synchronized with the IG solution.


- Under **User Rights menu** we can see the  what platform-level rights that they have for IdentityIQ.




## Identity classification:


- common classification:

 - employee
 - interns
 - temp worker
 - contractor
 - supplier
 - patner
 - bot : non human

- other classification:
 - permanent employee
 - fixed-term employee
 - subsidiary employee
 - subsidiary contractor
 - vendor


## Lab SailPoint IIQ: Identity Classification

- post logging into IIQ Interface navigate to identities tab --> identity warehouse --> on the right side we can see what type of identity it is.. like employee, contractor.. Its actually a configuration made in solution. Each identity comes from an authoritative source.

- The attributes differ from each identity based on the identity type. ex: job title only present for employees not for contractors.


- How this info is retrieved from authoritative sources??



## Authoritative sources - 1:


- we have some famous human resources information systems (HRIS)  like

 - workday
 - oracle
 - sap
 - talentspace

- all the above mentioned are used to manage identities


- once the identity is created in the authoritative sources the goal is to import it into IAG solutions.

- similarly when data is modified in human resources information systems(HRIS) they need to sync..


- This integration can be done in 2 ways


 - 1.**Flat file (.csv)**


- HRIS generates the flat file and this IAG solution ingests the file for creation, modification, delete..

- 2.**Direct connector**

- these are becoming more and more common. these are real connectors i.e., technical connectors b/w HRIS and IAG solutions


## Authoritative sources - 2:

- Data changes in identity authoritative sources can trigger IAM processes like joiner, mover, leaver processes
```
In identity authoritative source          In IAG                 Main actions performed

New Identity                              joiner process           create digital identity, generate login/pwsd,assign access rights, send notification to user and manager


Identity removal		                      	Leaver process	          Deactivate digital identity, remove access in applications

Job update				                           Mover process	           Delete old access rights, assign new access rights
```



## Lab SailPoint IIQ: Authoritative sources - 1:

-  Take 2 .csvs  in text format 1 for employees and another for contractors

- at the end of each file add // which will ignore that particular identity.


- Go to setup menu and click on Tasks


- click on **aggregate employees** and right click and click on **execute in background** & do the same for aggregate contractors.

- **Note**: Aggregate = fetch and load data from connected sources into SailPoint.


- After doing that go to **Task results** and we can see whether tasks for both employees and contractors are succeeded or not.


- Again remove the // from last line and we can  do the same aggregate employees & contractors. This time we can clearly see the difference that under **identities created** we can see the number as 1 for both employees and contractors as we exactly modified 1 for both.


- **Note**:  we wont be able to see the managers of all above users as it needs policy evaluation and identity linking which happens during **refresh identity cube**.
Refresh Identity Cube = Rebuild identity, apply rules, link relationships (like manager), calculate roles, policies, and risk scores.


- navigate to setup --> tasks --> search for refresh identity cube.


## employee departure process

- we need to keep // infront of .csv for employee then save and click on aggregate employees and run in background and we can see the task result where we can observe that **account links deleted** as 1.

- Through above process we have seen how identities have integrated into IAG solutions to manage iam life cycle.
- The files we modifies comes from HRIS in this case.

- **Note**: Need to configure this file path in server if its self hosting

## Lab SailPoint IIQ: Authoritative sources - 2:


- In this lab we r going to focus on modifying identity information.


- Modify the location of user from x to y and save and click on setup and tasks and click on aggregate employees and we can observe the location is changed to latest one.


- **Note**: In sailpoint we cant modify the data if we wants to change we need to do it from authoritative source i.e from HRIS. Its a good practice to respect this principle. But in few cases we need to modify data due to bugs, delays from HRIS we need to manually do this for temporary purpose. keep in mind that again if we do employee aggregate the changes which we manually modified and changes which are coming from authoritative source are matched then only old data will stay or else authoritative source data will be considered.

-  **example**:  from authoritative source  we received data where the identity data is paris but identity actual region is London we can manually change to London through below steps.

- settings --> global settings --> identity mappings --> region --> edit mode --> modify from read to temporary.


## Identity Life cycle:

<img width="800" height="480" alt="image" src="https://github.com/user-attachments/assets/5d9594c8-0061-405c-99a8-48d501c5fac8" />

- Identity Status
- <img width="4096" height="2017" alt="image" src="https://github.com/user-attachments/assets/19ece0f0-9bfe-4907-9731-e422d88a553b" />


## Identity Life cycle example 1:

- <img width="3944" height="1766" alt="image" src="https://github.com/user-attachments/assets/3f825a7d-9117-4366-a11d-acca1dec8d77" />

- Identity remains disabled till start date or unless until there is a bussiness need.
- 

## Identity Life cycle example 2:

- <img width="800" height="308" alt="image" src="https://github.com/user-attachments/assets/b091295f-9ce4-45fe-a37a-9b76c2808d3a" />

- we can clearly see the diff b/w example 1 & 2 that there is extra time span b/w contract end date and deactivation date providing additional time to complete remaining tasks.

## Identity Life cycle example 3:

- Contract employee needs to renew on time to time basis

- <img width="3264" height="1273" alt="image" src="https://github.com/user-attachments/assets/29ae2849-edb7-4890-9228-8f4fc841c765" />


## Lab SailPoint IIQ - Identity Life cycle

- How the deactivation of user in authoritative source can trigger the deactivation of identity in IAG solution along with their associated authorizations.

- Offboarding a user in a more granualr way

- In previous labs we seen how to delete a identity from sailpoint but in few cases we dont want to delete but instead we want to disable,archive,lock, deactivate..

- Instead of commenting(//) out whole identity this time we will be modifying the attribute which is **inactive from False to True** and do the **aggregation**. Observe under application accounts tab we can see status as active before performing above operation.

- Even after doing above things nothing will change. In sailpoint we need to configure  rules to instruct the solution that if the **inactive attribute is set to True** then the user rights shall be disabled.
- **Note**: In this demo we r not configuring the rules we r simply going with pre configured rules.

- To ensure that pre configured rules take into effect we need to navigate to tasks -->  search for **refresh with process events** and this task will refresh the identity based on the configured rules

## Unique Identifier- 1 :

- <img width="3264" height="1601" alt="image" src="https://github.com/user-attachments/assets/2f2e7d74-85d5-4fb6-be5e-7f0296ad2b73" />

- <img width="3264" height="1604" alt="image" src="https://github.com/user-attachments/assets/556e79f2-3163-437b-b828-a2c2a4c1ddaa" />
## Unique Identifier - 2 :

- <img width="3264" height="1574" alt="image" src="https://github.com/user-attachments/assets/3e8db751-5331-41d1-ae8a-24a876236fd8" />



## Identity Certification:

- 
 
























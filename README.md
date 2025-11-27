<img width="3264" height="1784" alt="image" src="https://github.com/user-attachments/assets/e94eb397-4328-47c5-8af9-2704774ee0d0" /># Sail Point
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

- **Identity Certification** : Checking if users have the right access right now.

- **Identity Recertification** : Doing that check again at regular intervals (e.g., every 3 months, 6 months, or yearly).

- <img width="800" height="404" alt="image" src="https://github.com/user-attachments/assets/ed65fa13-9c87-4e7c-97b5-dde0dc907d9d" />

- workflow: compliance manager --> manager --> IAG


## Access rights Management Capabilities:

- <img width="3264" height="2448" alt="image" src="https://github.com/user-attachments/assets/a817625b-e8fc-4569-8d17-85f85f4708ae" />

- How to assign the access rights to identities and how this access rights are managed to meet the challenges faced by bussinesses and comply with security requirements??

- Access management includes 8 major capabilities to support access management processes.

## Access rights Models -  RBAC : 1:
- Role: Collection of permissions. all users receive permissions only through the roles to which they are assigned in IG solution.

- Instead of assigning individual permissions to each user, SailPoint groups permissions into roles.

- Identity → Role → Entitlement(permissions/privilige)

### RBAC Implementation:
- <img width="3264" height="1879" alt="image" src="https://github.com/user-attachments/assets/de54573c-67f3-48e3-975c-0391b5fd416b" />

- **Identity** --> user(sai),
-  **Role** --> A bundle of related access(devops engg  role ),
- **Access profile** (CI/CD  access profile..includes Jenkins, GitHub Actions, Kubernetes cluster access) --> A set of entitlements(permissions) grouped together,
- **Entitlement** --> actual permission in system jenkins build pipelines access, k8s deploy pods access, github repo write access,
- **Source** ---> The system where the permission lives (jenkins,github..)

- **Drawbacks**: maintenance of larger roles if org is big.


##  Access rights Models - ABAC : Attribute based Access Control(fine-grained control):

- This model controls access by evaluating rules against attributes:
 - user attributes
 - environmental attributes
 - resource attributes
- The rules are configured directly within the  target applications.
- Retrieval of attributes is achieved at the time of authentication.
- <img width="3264" height="1821" alt="image" src="https://github.com/user-attachments/assets/2d12bbfa-7554-4455-9464-c39f508a74c7" />
- <img width="3264" height="1630" alt="image" src="https://github.com/user-attachments/assets/826b7e9d-f1dd-4264-85d6-e6a79677bf6c" />


##  Access rights Models:  RBAC-A

- Integrating **attributes** with **RBAC** model was made possible and allowed the creation of an even more advanced model which is **RBAC-A**

- Role assignment is made dynamically by evaluating rules within the IAG solution against attributes.

- **Example Rule**: If Department = Finance AND Location = Hyderabad → Assign Finance Analyst Role automatically.

So RBAC-A = RBAC + Attribute-based logic for dynamic role assignment.
-  <img width="3264" height="1482" alt="image" src="https://github.com/user-attachments/assets/2a602d0c-bb48-4079-bd5a-a6c683dcde22" />

### RBAC (Traditional)

- User → Assigned Role → Gets Permissions.
Example:

- Role = Finance Analyst
- Permissions = SAP Read, SAP Write.

- **Problem**: If user changes department, you must manually change the role.

- **RBAC-A (Dynamic)**

- User → Attributes → Rules → Role → Permissions.
**Example:**

- **Attributes**:

- Department = Finance
- Location = Hyderabad

- **Rule**:

- IF Department = Finance AND Location = Hyderabad → Assign Finance Analyst Role.

## Role Management 1:

- <img width="3264" height="1801" alt="image" src="https://github.com/user-attachments/assets/044eab0a-889e-4d79-abbd-25eba9964c61" />

- **Name & Description**: Uniquely identify and understand its scope.
- **Role Composition**: Access rights granted by the role
- **Owner**: Responsible of the role model
- **Role criticality**: Level of criticality of the rights granted
- **Population authorized**: Identities that can benefit from the role
- **Approval workflow**: Approvals needed to obtain role
- **SoD (Segregation of duties) toxicity**: Incompatibilities with other roles.(detects toxic combinations of entitlements)

 ## Role management 2:
 - **Focus on role composition**: This will be done via 2 approaches
 
 ### **Top-Down**
 - Develop a group of roles based on job functionalities and needs while keeping in mind the principles of SOD and least privilege.

 ### Bottom-Up
 - Analyze user access data to identify clusters of users with similar permissions and organize them into appropriate roles.

### Role life cycle:

- Role creation --> Role update --> Role decomissioning

- <img width="3264" height="1761" alt="image" src="https://github.com/user-attachments/assets/c35f1a98-0c6c-4efa-a5f6-8cf6e42ccb40" />

- <img width="3264" height="1761" alt="image" src="https://github.com/user-attachments/assets/4ccdd8b5-94f6-4efb-a1cb-63381f8d4122" />


## Access request and workflow:

- <img width="3264" height="1853" alt="image" src="https://github.com/user-attachments/assets/33e14489-8d0b-43a2-a97e-9644f609e01b" />

- <img width="3264" height="1784" alt="image" src="https://github.com/user-attachments/assets/5c6cc445-5785-44fa-b8bc-4f3c82681653" />



## LAB SailPoint IIQ: Application configuration and request:

- In this lab we r going to modify the configuration of an application to add additional entitlement to this application. In this lab we already pre-configured a  number of applications

- We can see the list of applications under **Applications Tab** --> **Application Definition**.

- So the idea is to revoke/grant rights for users on this applications.

- Click on any application under this and click on **configuration** tab and click on **schema** 

-  We can see the list of applications under **Applications Tab** --> **Entitlement catalog**.

-  In the below sheet we can see list of entitlements available for time tracking application.
    
- <img width="3264" height="959" alt="image" src="https://github.com/user-attachments/assets/0dbcdeff-1a08-4ee8-8394-58505e19507f" />

- If we want to add any  entitlement to individual for particular application we need to navigate to **applications** tab and click on **Entitlement catalog** and click on **add new entitlement** and then choose **application** and select **attribute** that corresponds to **entitlement** and fill the **value** (Ex: we need  to add reporting  permission to individual then we need to fill **Reporting** under value ) and add description(configure reports) under **Requestable** tab and save it.

- In reality above entitlement wont be created yet it needs validation workflows for approval. But if we use admin account for above activity we can approve request for ourself by navigating to **Home page** and click on **approvals**  and approve it. Post that just verify the same by navigating to Entitlement catalog and type the application name we can the entitlement which we created and approved now.


- In above we just created entitlement and now we will assign this to identity by navigating to **left menu** --> **Manage Access** --> **Manage User Access** and search  users and select and click next.

- In 2nd step search  access and use filters option for selecting entitlement in our case its reporting and click on Next and then review and submit. Even after submitting the request entitlement wont be assigned to user immediately. we can cross verify the same by navigating to **identity --> Identity warehouse** --> **user name --> Application Accounts** and under this we can clearly see reporting entitlement is not yet assigned. But under events we can see the request as is it is pending under approval by user manager which we can see under the home page --> track my requests.

- Login to manager account and approve the same and post that manager can manage the identites by navigating to Managing Identity --> View identity 

## LAB SailPoint IIQ: Automatic Role Configuration:

- Click on **setup** --> **Roles** --> Click On **Add**

- I want to give time tracking reporting rights to the department **executive management**  under Assignment rule  which can be done by below

- Create role and assign necessary entitlements

- <img width="3264" height="1717" alt="image" src="https://github.com/user-attachments/assets/113b1f93-4c1d-467e-8081-d4a82336de58" />

## Role Mining
- Role Mining refers to the process of analyzing access rights and permission data from existing system or application.

- This process is used to identify groups of users who share similar permissions and group them into roles or user groups.

- The goal here is to create roles that simplify the onboarding process for new users.

- **Scenario**: Finance Department

- You analyze access data for 50 users in the Finance team.
- You find that 30 users have these common entitlements:

 -  View_Invoice
 - Approve_Payment
 - Access_Finance_Reports



- **Role Mining Outcome**

- Instead of assigning these 3 entitlements individually to each user, you create a role called:

- Finance Analyst Role

- Includes: View_Invoice, Approve_Payment, Access_Finance_Reports. Assign this role to those 30 users.


 ### Top-Down Approach

- Roles are designed based on business functions and job responsibilities.

### Bottom-Up Approach

- Roles are created by analyzing existing user access patterns.

## Lab SailPointIIQ :  Role Mining


## Segregation od Duties: This helps to ensure that no individual has too much control over single process. Segregation of Duties (SoD) exists—to prevent one person from having conflicting powers that enable fraud.

- <img width="3264" height="1833" alt="image" src="https://github.com/user-attachments/assets/6d7b69f6-bc64-4f34-b89c-f0fa274bf8d9" />

- 


-  


- 


- 






-    





 

























# Study Guide for Exam AZ-500: Microsoft Azure Security Technologies


## Manage identity and access (30-35%)
### Manage Azure Active Directory identities
| Term | Description |
|---|---|
| [Azure Active Directory (AD)](https://docs.microsoft.com/en-us/learn/modules/manage-users-and-groups-in-aad/2-create-aad) | **Directories, subscriptions, and users** - Microsoft offers several cloud-based offerings today - all of which can use Azure AD to identify users and control access. When a company or organization signs up to use one of these offerings, they are assigned a default  ***directory***, an instance of Azure AD. This directory holds the users and groups that will have access to each of the services the company has purchased. This default directory can be referred to as a  ***tenant***. A tenant represents the organization and the default directory assigned to it.<br/> <br/> ***Subscriptions***  in Azure are both a billing entity and a security boundary. Resources such as virtual machines, websites, and databases are associated with a single subscription. Each subscription also has a single account  ***owner***  responsible for any charges incurred by resources in that subscription. If your organization wants a subscription billed to another account, you can transfer the subscription. A subscription is associated with a  **single Azure AD directory**. Multiple subscriptions can trust the same directory, but a subscription can only trust one directory. <br/> <br/> Users and groups can be added to multiple subscriptions - this allows the user to create, control, and access resources in the subscription. When you add a user to a subscription, the user must be known to the associated directory as shown in the following image. <br/> ![Conceptual art showing users, directories, and subscriptions in Azure.](https://docs.microsoft.com/en-us/learn/modules/manage-users-and-groups-in-aad/media/2-users-subs-and-directories.png)<br/> If you belong to multiple directories, you can switch the current directory you are working in through the  **Directory + subscription**  button in the Azure portal header.<br/> ![Screenshot showing the Directory selection dialog in Azure portal.](https://docs.microsoft.com/en-us/learn/modules/manage-users-and-groups-in-aad/media/2-directory-and-subscription.png)<br/> You can also decide how the default directory is selected: last visited or a specific directory. You can also set the default filter for displayed subscriptions. Default filters are useful if you have access to several subscriptions but typically only work in a few of them.|
| [Built-in Azure AD roles](https://docs.microsoft.com/en-us/learn/modules/manage-users-and-groups-in-aad/5-manage-aad-roles) | Azure AD provides several  _built-in roles_  to cover the most common security scenarios. To understand how the roles work, let's examine three roles that apply to all resource types:<br/><br/>&bull; **Owner**, which has full access to all resources, including the right to delegate access to others.<br/>&bull; **Contributor**, which can create and manage all types of Azure resources but can’t grant access to others.<br/> &bull; **Reader**, which can view existing Azure resources. <br/><br/> Each role is a set of properties defined in a JavaScript Object Notation (JSON) file. This role definition includes a  **Name**,  **ID**, and  **Description**. It also includes the allowable permissions (**Actions**), denied permissions (**NotActions**), and scope (for example, read access) for the role. For the Owner role, that means all actions, indicated by an asterisk (*); no denied actions; and all scopes, indicated by a forward slash (/).<br/><br/>A role definition is a collection of permissions. A **role definition** lists the operations that can be performed, such as read, write, and delete. It can also list the operations that can't be performed or operations related to underlying data and has the following structure.<br/>**Id** = Unique identifier for the role, assigned by Azure.<br/>**IsCustom** = True if a custom role, False if a built-in role.<br/>**Description** = A readable description of the role.<br/>**Actions []** = Allowed permissions, * indicates all.<br/>**NotActions []** = Denied permissions.<br/>**DataActions []** = Specific allowed permissions as applied to data, for example: _Microsoft.Storage/storageAccounts/blobServices/containers/blobs/read_<br/>**NotDataActions []** = Specific denied permissions as applied to data.<br/>**AssignableScopes []** = Scopes where this role applies. / indicates global, but can reach into a hierarchical tree.|
| [Azure AD users](https://docs.microsoft.com/en-us/learn/modules/manage-users-and-groups-in-aad/3-users) | Typically, Azure AD defines users in three ways: <br/>**1 - Cloud identities**  - These users exist only in Azure AD. Examples are administrator accounts and users that you manage yourself. Their source is  **Azure Active Directory**  or  **External Azure Active Directory**  if the user is defined in another Azure AD instance but needs access to subscription resources controlled by this directory. When these accounts are removed from the primary directory, they are deleted. <br/> **2 - Directory-synchronized identities**  - These users exist in an on-premises Active Directory. A synchronization activity that occurs via  **Azure AD Connect**  brings these users in to Azure. Their source is  **Windows Server AD**. <br/> **3 - Guest users**  - These users exist outside Azure. Examples are accounts from other cloud providers and Microsoft accounts, such as an Xbox LIVE account. Their source is  **Invited user**. This type of account is useful when external vendors or contractors need access to your Azure resources. Once their help is no longer necessary, you can remove the account and all of their access.<br/><br/>You can add cloud identities to Azure AD in multiple ways:<br/> <br/> &bull; Syncing an on-premises Windows Server Active Directory <br/> &bull; Using the Azure portal <br/> &bull; Using the command line<br/><br/> **Azure AD Connect** is a separate service that allows you to synchronize a traditional Active Directory with your Azure AD instance. This is how most enterprise customers add users to the directory. The advantage to this approach is users can use single sign-on (SSO) to access local and cloud-based resources.|
| [Group and membership](https://docs.microsoft.com/en-us/learn/modules/manage-users-and-groups-in-aad/4-groups) | An Azure AD group helps organize users making it easier to manage permissions. Using groups lets the resource owner (or Azure AD directory owner), assign a set of access permissions to all the members of the group, instead of having to provide the rights one-by-one. Groups allow us to define a security boundary and then add and remove specific users to grant or deny access with a minimum amount of effort. Even better, Azure AD supports the ability to define membership based on rules - such as what department a user works in, or the job title they have.  <br/><br/>Azure AD allows you to define two different types of groups.<br/>**1 - Security groups**. These are the most common and are used to manage member and computer access to shared resources for a group of users. For example, you can create a security group for a specific security policy. By doing it this way, you can give a set of permissions to all the members at once, instead of having to add permissions to each member individually. This option requires an Azure AD administrator.<br/>**2 - Microsoft 365 groups**. These groups provide collaboration opportunities by giving members access to a shared mailbox, calendar, files, SharePoint site, and more. This option also lets you give people outside of your organization access to the group. This option is available to users as well as admins. <br/><br/> ![Screenshot of the Create Group feature in the Azure portal.](https://docs.microsoft.com/en-us/learn/modules/manage-users-and-groups-in-aad/media/4-add-group-portal.png)<br/>Group "membership type" can be of the following 3 types:<br/>1.  **Assigned (static)**. The group will contain specific users or groups that you select.<br/>2.  **Dynamic user**. You create rules based on characteristics to enable attribute-based dynamic memberships for groups. For example, if a user’s department is Sales, that user will be dynamically assigned to the Sales group. Security groups can be used for either devices or users, but Microsoft 365 Groups can be only used for user groups. If the user's department changes in the future, they are automatically removed from the group. This feature requires an Azure AD Premium P1 license. <br/>3.  **Dynamic device**. You create rules based on characteristics to enable attribute-based dynamic memberships for groups. For example, if a user’s device is associated with the Service department, that device will be dynamically assigned to the Service group. Security groups can be used for either devices or users, but Microsoft 365 Groups can be only used for user groups. If the device's association with a particular department changes in the future, it is automatically removed from the group. This feature requires an Azure AD Premium P1 license.|
| [Administrative Units in Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/roles/administrative-units) | An administrative unit is an Azure AD resource that can be a container for other Azure AD resources. **An administrative unit can contain only users, groups, or devices.** Administrative units restrict permissions in a role to any portion of your organization that you define.  <br/><br/> For example, a large university that's made up of many autonomous schools (School of Business, School of Engineering, and so on). Each school has a team of IT admins who control access, manage users, and set policies for their school.<br/> <br/>A central administrator could: <br/>-   Create an administrative unit for the School of Business.<br/>-   Populate the administrative unit with only students and staff within the School of Business.<br/>-   Create a role with administrative permissions over only Azure AD users in the School of Business administrative unit.<br/>-   Add the business school IT team to the role, along with its scope.<br/><br/>![Screenshot of Devices and Administrative units page with Remove from administrative unit option.](https://docs.microsoft.com/en-us/azure/active-directory/roles/media/administrative-units/admin-unit-overview.png)|
| [Authentication options decision tree](https://docs.microsoft.com/en-us/azure/active-directory/hybrid/choose-ad-authn) | xxx |
| [Password hash synchronization](https://docs.microsoft.com/en-us/azure/active-directory/hybrid/whatis-phs) | xxx |
| [Enable password hash synchronization](https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-password-hash-synchronization) | xxx |
| [Pass-through authentication](https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-pta-how-it-works) | xxx |
| [Azure AD Pass-through Authentication](https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-pta-quick-start) | xxx |
| [Passwordless](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-authentication-passwordless-deployment) | xxx |
| [Passwordless Phone](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-authentication-passwordless-phone) | xxx |
| [Passwordless Security Key](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-authentication-passwordless-security-key) | xxx |
| [Passwordless Launch Blog](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/passwordless-authentication-is-now-generally-available/ba-p/1994700) | xxx |
| [Microsoft Identity Platform ](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-overview) | xxx |
| [Azure AD pricing ](https://azure.microsoft.com/en-us/pricing/details/active-directory/) | xxx |

### Configure secure access by using Azure AD

| Term | Description |
|---|---|
| [Privileged Identity Management (PIM) ](https://docs.microsoft.com/en-us/learn/modules/protect-against-security-threats-azure) | xxx |
| [Assign Azure AD roles in PIM ](https://docs.microsoft.com/en-us/azure/active-directory/privileged-identity-management/pim-how-to-add-role-to-user) | xxx |
| [Getting started in PIM](https://docs.microsoft.com/en-us/azure/active-directory/privileged-identity-management/pim-getting-started) | xxx |
| [PIM configuration settings ](https://docs.microsoft.com/en-us/azure/active-directory/privileged-identity-management/pim-how-to-change-default-settings) | xxx |
| [Building a Conditional Access policy ](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/concept-conditional-access-policies) | xxx |
| [Activate and configure PIM—demo ](https://docs.microsoft.com/en-us/azure/active-directory/privileged-identity-management/pim-how-to-add-role-to-user) | xxx |
| [Azure Multi-Factor Authentication ](https://docs.microsoft.com/en-us/learn/modules/secure-aad-users-with-mfa/2-azure-multi-factor-authentication) | xxx |
| [Access reviews in Azure AD ](https://docs.microsoft.com/en-us/azure/active-directory/governance/create-access-review) | xxx |
| [Access review in PIM ](https://docs.microsoft.com/en-us/azure/active-directory/privileged-identity-management/pim-create-azure-ad-roles-and-resource-roles-review) | xxx |

### Manage application access

| Term | Description |
|---|---|
| [App registration](https://docs.microsoft.com/en-us/learn/modules/secure-app-with-oidc-and-azure-ad/3-create-aad-register-app) | xxx |
| [Azure AD consent framework](https://docs.microsoft.com/en-us/azure/active-directory/develop/consent-framework) | xxx |
| [Managed identities in Azure](https://docs.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/overview#:%7E:text=Managed%20identities%20for%20Azure%20resources%20is%20a%20feature%20of%20Azure%20Active%20Directory.&text=The%20feature%20provides%20Azure%20services,any%20credentials%20in%20your%20code) | xxx |

### Manage access control

| Term | Description |
|---|---|
| [Role-based access control (RBAC)](https://docs.microsoft.com/en-us/learn/modules/secure-azure-resources-with-rbac/2-rbac-overview) | xxx |
| [RBAC scope](https://docs.microsoft.com/en-us/learn/modules/secure-azure-resources-with-rbac/2-rbac-overview) | xxx |
| [Built-in Azure RBAC roles](https://docs.microsoft.com/en-us/learn/modules/manage-subscription-access-azure-rbac/2-identify-appropriate-role-assign) | xxx |
| [Create or update Azure custom roles ](https://docs.microsoft.com/en-us/azure/role-based-access-control/custom-roles-portal) | xxx |
| [Configure custom RBAC roles—demo ](https://docs.microsoft.com/en-us/azure/role-based-access-control/custom-roles-portal) | xxx |
| [Resource locks ](https://docs.microsoft.com/en-us/learn/modules/control-and-organize-with-azure-resource-manager/6-use-resource-locks-to-protect-resources) | xxx |

## Implement platform protection (15-20%)

### Implement advanced network security

| Term | Description |
|---|---|
| [Security](https://docs.microsoft.com/en-us/learn/modules/protect-against-security-threats-azure/) | xxx |
| [Network security groups (NSGs)](https://docs.microsoft.com/en-us/learn/modules/secure-and-isolate-with-nsg-and-service-endpoints/2-network-security-groups) | xxx |
| [NSG deployment scenarios](https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview) | xxx |
| [Application security groups (ASGs)](https://docs.microsoft.com/en-us/learn/modules/secure-and-isolate-with-nsg-and-service-endpoints/2-network-security-groups) | xxx |
| [Configure NSGs and ASGs—demo](https://docs.microsoft.com/en-us/azure/virtual-network/manage-network-security-group) | xxx |
| [Azure Firewall](https://docs.microsoft.com/en-us/azure/firewall/features) | xxx |
| [Deploy and configure Azure Firewall](https://docs.microsoft.com/en-us/azure/firewall/tutorial-firewall-deploy-portal) | xxx |
| [Azure Web Application Firewall (WAF)](https://docs.microsoft.com/en-us/azure/web-application-firewall/ag/ag-overview) | xxx |
| [Azure Front Door](https://docs.microsoft.com/en-us/azure/frontdoor/front-door-overview) | xxx |
| [Azure Bastion service](https://docs.microsoft.com/en-us/azure/bastion/bastion-overview) | xxx |
| [Create an Azure Bastion host](https://docs.microsoft.com/en-us/azure/bastion/tutorial-create-host-portal) | xxx |
| [Service endpoints](https://docs.microsoft.com/en-us/learn/modules/secure-and-isolate-with-nsg-and-service-endpoints/4-vnet-service-endpoints) | xxx |
| [Distributed denial of service (DDoS) protection](https://docs.microsoft.com/en-us/learn/modules/protect-against-security-threats-azure/) | xxx |

### Configure advanced security for compute

| Term | Description |
|---|---|
| [Endpoint protection](https://docs.microsoft.com/en-us/azure/defender-for-cloud/endpoint-protection-recommendations-technical) | xxx |
| [Implement vulnerability management](https://docs.microsoft.com/en-us/azure/defender-for-cloud/deploy-vulnerability-assessment-vm) | xxx |
| [Update Management](https://docs.microsoft.com/en-us/azure/automation/update-management/overview) | xxx |
| [Configure a TLS/SSL certificate](https://docs.microsoft.com/en-us/azure/app-service/configure-ssl-certificate) | xxx |
| [Configure security for different containers](https://docs.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-introduction&tabs=defender-for-container-arch-aks) | xxx |
| [Access and identity options for Azure Kubernetes Service (AKS)](https://docs.microsoft.com/en-us/azure/aks/concepts-identity) | xxx |
| [Configure security for container registry](https://docs.microsoft.com/en-us/azure/container-registry/container-registry-authentication&tabs=azure-cli) | xxx |
| [Network concepts for applications in AKS](https://docs.microsoft.com/en-us/azure/aks/concepts-network) | xxx |

## Manage security operations (25-30%)

### Monitor security by using Azure Monitor

| Term | Description |
|---|---|
| [Azure Monitor](https://docs.microsoft.com/en-us/learn/modules/analyze-infrastructure-with-azure-monitor-logs/2-features-azure-monitor-log) | xxx |
| [Alerts](https://docs.microsoft.com/en-us/learn/modules/incident-response-with-alerting-on-azure/2-explore-azure-monitor-alert-types) | xxx |
| [Create, view, and manage log alerts using Azure Monitor](https://docs.microsoft.com/en-us/azure/azure-monitor/alerts/alerts-log) | xxx |
| [Configuring diagnostic logging and log retention](https://docs.microsoft.com/en-us/azure/azure-monitor/essentials/diagnostic-settings) | xxx |

### Monitor security by using Azure Security Center

| Term | Description |
|---|---|
| [Overview of Azure Security Center](https://azure.microsoft.com/en-us/pricing/details/defender-for-cloud) | xxx |
| [Monitor security with Azure Security Center](https://docs.microsoft.com/en-us/learn/modules/identify-threats-with-azure-security-center/5-analyze-recommendations) | xxx |
| [Centralized policy management](https://docs.microsoft.com/en-us/learn/modules/identify-threats-with-azure-security-center/4-policy-management) | xxx |
| [Configure security settings by using Azure Policy](https://docs.microsoft.com/en-us/azure/defender-for-cloud/tutorial-security-policy) | xxx |
| [Vulnerability scanner](https://docs.microsoft.com/en-us/azure/defender-for-cloud/deploy-vulnerability-assessment-vm) | xxx |
| [Enable JIT VM access](https://docs.microsoft.com/en-us/learn/modules/secure-vms-with-azure-security-center/3-exercise-jit-vm-access) | xxx |
| [Azure Security Center—demo](https://docs.microsoft.com/en-us/azure/defender-for-cloud/tutorial-protect-resources) | xxx |

### Monitor security by using Azure Sentinel

| Term | Description |
|---|---|
| [Azure Sentinel](https://docs.microsoft.com/en-us/azure/sentinel/overview) | xxx |
| [Create and customize alerts in Azure Sentinel](https://docs.microsoft.com/en-us/azure/sentinel/detect-threats-built-in) | xxx |
| [Connect data sources](https://docs.microsoft.com/en-us/azure/sentinel/connect-data-sources) | xxx |
| [Create incidents from alerts](https://docs.microsoft.com/en-us/azure/sentinel/create-incidents-from-alerts) | xxx |
| [Investigate incidents with Azure Sentinel](https://docs.microsoft.com/en-us/azure/sentinel/investigate-cases) | xxx |
| [Configure a playbook for a security event](https://docs.microsoft.com/en-us/azure/sentinel/tutorial-respond-threats-playbook) | xxx |

### Configure security policies

| Term | Description |
|---|---|
| [Azure Policy](https://docs.microsoft.com/en-us/azure/governance/policy/overview) | xxx |
| [Create and manage policies to enforce compliance](https://docs.microsoft.com/en-us/azure/governance/policy/tutorials/create-and-manage) | xxx |
| [Create a custom policy definition](https://docs.microsoft.com/en-us/azure/governance/policy/tutorials/create-custom-policy-definition) | xxx |
| [Deploy an Azure Policy—demo](https://docs.microsoft.com/en-us/azure/governance/policy/tutorials/create-and-manage) | xxx |
| [Azure Blueprint](https://docs.microsoft.com/en-us/learn/modules/build-cloud-governance-strategy-azure/) | xxx |
| [Create and assign blueprints](https://docs.microsoft.com/en-us/azure/governance/blueprints/create-blueprint-portal) | xxx |

## Secure data and applications (25–30%)

### Configure security for storage

| Term | Description |
|---|---|
| [Azure Storage overview](https://docs.microsoft.com/en-us/learn/modules/create-azure-storage-account/2-decide-how-many-storage-accounts-you-need) | xxx |
| [Authorization options for Azure Storage](https://docs.microsoft.com/en-us/azure/storage/common/authorize-data-access) | xxx |
| [Azure AD Storage Authentication](https://docs.microsoft.com/en-us/azure/storage/blobs/authorize-access-azure-active-directory) | xxx |
| [Shared access signature (SAS)](https://docs.microsoft.com/en-us/rest/api/storageservices/delegate-access-with-shared-access-signature) | xxx |
| [Create a user delegation SAS](https://docs.microsoft.com/en-us/rest/api/storageservices/create-user-delegation-sas) | xxx |
| [Azure AD Domain Services](https://docs.microsoft.com/en-us/azure/active-directory-domain-services/overview) | xxx |
| [Azure Storage Service Encryption (SSE)](https://docs.microsoft.com/en-us/learn/modules/azure-well-architected-security/5-encryption) | xxx |
| [Configure encryption key management](https://docs.microsoft.com/en-us/learn/modules/azure-well-architected-security/5-encryption) | xxx |

### Configure security for databases

| Term | Description |
|---|---|
| [Enable database auditing](https://docs.microsoft.com/en-us/learn/modules/create-security-baselines/5-create-an-azure-sql-database-baseline) | xxx |
| [Server-level vs. database-level auditing policy](https://docs.microsoft.com/en-us/azure/azure-sql/database/auditing-overview) | xxx |
| [Configure Azure SQL Database Advanced Threat Protection (ATP)](https://docs.microsoft.com/en-us/learn/modules/create-security-baselines/5-create-an-azure-sql-database-baseline) | xxx |
| [Advanced Data Security (ADS)](https://docs.microsoft.com/en-us/azure/azure-sql/database/azure-defender-for-sql) | xxx |
| [Advanced Threat Protection](https://docs.microsoft.com/en-us/learn/modules/protect-against-security-threats-azure/) | xxx |
| [SQL Database authentication](https://docs.microsoft.com/en-us/azure/azure-sql/database/logins-create-manage) | xxx |
| [Implement database encryption through transparent data encryption (TDE)](https://docs.microsoft.com/en-us/azure/azure-sql/database/transparent-data-encryption-tde-overview?tabs=azure-portal#manage-transparent-data-encryption) | xxx |
| [Configure Always Encrypted by using Azure Key Vault](https://docs.microsoft.com/en-us/azure/azure-sql/database/always-encrypted-azure-key-vault-configure) | xxx |

### Configure and manage Azure Key Vault

| Term | Description |
|---|---|
| [Implement and configure Key Vault](https://docs.microsoft.com/en-us/learn/modules/manage-secrets-with-azure-key-vault/2-what-is-key-vault) | xxx |
| [Key rotation](https://docs.microsoft.com/en-us/azure/key-vault/secrets/tutorial-rotation-dual&tabs=azure-cli) | xxx |
| [Key Vault access and permissions](https://docs.microsoft.com/en-us/azure/key-vault/general/security-features) | xxx |
| [Management plane and access plane for Key Vault—demo](https://docs.microsoft.com/en-us/azure/key-vault/general/quick-create-portal) | xxx |


---
## Supplemental Links:
[Microsoft AZ-500 page that includes free training, skills measured PDF, and exam details](https://docs.microsoft.com/en-us/learn/certifications/exams/az-500)

[Microsoft Enterprise Skills Initiative Study Guide for AZ-500](https://aka.ms/ESIStudyGuide_AZ-900)

[WhizLabs AZ-500](https://www.whizlabs.com/microsoft-azure-certification-az-500)

---
<br/> &bull;
Bold: **CanNotDelete**
Bold + Italitcs ***initiatives***

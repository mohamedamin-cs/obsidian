#### [[Active Directory]]:
**Active Directory Domain Service (AD DS)**. This service acts as a catalogue that holds the information of all of the "objects" that exist on your network. Amongst the many objects supported by AD, we have users, groups, machines, printers, shares and many others.
___
**[[Objects]]**:
1. **Users**: [[security principals]] (they can be authenticated by the domain and can be assigned privileges over **resources** like files or printers).
	types :
	- **peoples** : persons in your organisation.
	- **Services** : they will only have the privileges needed to run their specific service(IIS,Mysql...).
2. **Machines** :
	- for every computer that joins the Active Directory domain, a machine object will be created.
	- Machine Account passwords are automatically rotated out and are generally comprised of 120 random characters.
3. **Security Groups** :
	- assign access rights to files or other resources to entire groups instead of single users.
	- security principals.
	- Groups can have both users and machines as members.	![[Screenshot_20250703_002726.png]]
___
**Organizational Units (OUs)** :container objects that allow you to classify users and machines.
![[Pasted image 20250703003011.png]]
- **Builtin:** Contains default groups available to any Windows host.
- **Computers:** Any machine joining the network will be put here by default. You can move them if needed.
- **[[Domain Controllers]]:** Default OU that contains the DCs in your network.
- **Users:** Default users and groups that apply to a domain-wide context.
- **Managed Service Accounts:** Holds accounts used by services in your Windows domain.
___
**Deleting extra OUs and users**: view -> advanced features -> uncheck "protect objects from accidental deletion"
**Delegation**: give specific users some control over some OUs.  Delegate Control -> add -> check names 
- Set-ADAccountPassword sophie -Reset -NewPassword (Read-Host -AsSecureString -Prompt 'New Password') -Verbose : use [[powershell]] to reset password 
-  Set-ADUser -ChangePasswordAtLogon $true -Identity sophie -Verbose :forces the user `sophie` to change her password the next time she logs
___
####  Default OU Behavior in Active Directory
- When a machine joins a domain, it **automatically goes into the `Computers` container**, unless configured otherwise.
- This default container is **not an Organizational Unit (OU)**, so **Group Policies (GPOs)** cannot be linked directly to it.
#### Device Categories
1. **Workstations**
- Used by regular users for daily tasks.
- Must not have **privileged users** logging into them.
- Should have **user-focused policies** (e.g., USB restrictions, software lockdowns).
2. **Servers**
- Provide services (e.g., file storage, web hosting).
- Require **different policies** for uptime, security, and access.
3. **Domain Controllers (DCs)**
- Most sensitive devices in the domain.
- Contain **hashed credentials** of all users.
- Managed separately (Windows creates a default OU for them).
___
### Group Policy Object ([[GPO]]) 
- **collection of settings** applied to users or computers.
- Managed through the **Group Policy Management Console (GPMC)**.
- Group Policy management -> Group Policy Objects → Right-click GPO → Edit
___
### **Windows Domain Authentication Protocols**
1. **[[Kerberos]] Authentication:**
	- **Default protocol** on modern Windows domains
	- Uses **tickets** to authenticate without repeatedly transmitting credentials
	- More **secure** and **efficient** than NetNTLM
	### **Key Concepts**

	- **KDC**: Provides tickets, part of the Domain Controller
    
	- **TGT**: Proves user identity, used to request more tickets
    
	- **TGS**: Grants access to a specific service
	    
	- **SPN**: Identifies the service the user wants to access
    
	- **krbtgt**: Special user account used to encrypt TGTs
	![[Pasted image 20250703005906.png]]
	![[Pasted image 20250703010407.png]]
	![[Pasted image 20250703010414.png]]
	
2. **[[NetNTLM]] :**

	![[Pasted image 20250703011153.png]]
___
### Trees, Forests and Trusts
	Forest
	├── Tree 1: thm.local
	│   ├── uk.thm.local
	│   └── us.thm.local
	└── Tree 2: mht.local
	    ├── eu.mht.local
	    └── asia.mht.local

- A **forest = multiple trees** (even with different namespaces). 
- Forests allow **central trust and coordination**, but **separate administration**.
**Types of trusts**: 
- **One-Way Trust**:
    - **Domain A trusts Domain B**
    - B users can access A’s resources (if authorized)
    - A users **cannot** access B’s resources
- **Two-Way Trust**:
    - Both domains **mutually trust** each other
    - Users can access each other’s resources (if authorized)
___
Connect via [[RDP]] : [[remmina]]
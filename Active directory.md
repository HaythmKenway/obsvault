 https://www.youtube.com/watch?v=Tz94PZ1cWDo&list=PLFtZrY0nsVYS2fTvuW7uAGVUqf24fp7NO&index=1&t=28s

SAM Db
it is a database used to store username and password 
it is a default database and it is located in C:\\Windows\\system32\\config\\SAM


## Workgroup
all computers in workgroup uses sam  database by default

### Domain Model
The database of Domain model is NTDS
the acronym of NTDS is new technology directory services
it is a manual database
C:\windows\\ntds\\ntds.dit
it stores username and password
It is a centralized Database
![[Pasted image 20230531095839.png]]

### Converting workgroup to Domain
we can convert a workgroup to domain using a active directory domain services

Need for centralised database?
easy administration


 ## work group and Domain

1) What is Domain?
 it is a collection of user server groups and computer uses common database in an organization 
 this organisation is called domain.

![[Pasted image 20230531141235.png]]

here ekascloud.com is domain
ntds is database
kumar and administrator are users


###  Domain controller
A computer running ADDS
A computer with the NTDS Database (exist)

### Adding a computer to domain

step 1: create an user for computer
>	open dsa.msc (Active Directory Users and Computers)
> 	create a new user in  the user folder
> 	![[Pasted image 20230531143817.png]]![[Pasted image 20230531143840.png]]

After inistalling adds domain is first created then domain controller is added

step 2: joining the computer in adds network
>![[Pasted image 20230531143956.png]]
> add the dns ip address into preffered dns on the client machine by following the step
> after that we will be able to join the client machine into active directory domain services
>
>open ncpa.cpl to modify the network settings
> click on the network and open properties
> ![[Pasted image 20230531144357.png]]
> 
> ![[Pasted image 20230531144420.png]]
> set the ip address of the domain controller (dns server)
> open sysdm.cpl
> ![[Pasted image 20230531144538.png]]
> add domain name and the system is added to the active directory domain services
> ![[Pasted image 20230531144642.png]]
> now we can see that the client is added to the domain
> 

users can be added to various groups to get the privilege level for performing various actions withing the limit

   ---
### NTDS.DIT file partitions

Objects:-
accounts in AD Database

There are many types of objects
+ user object (used to login)
+ Group object (to link other object)
+ Computer object (Identify computers in domain)
+ Contact object (Used to store user information)

Classes:-
classes are used to define objects
eg userclass,group class

### Attributes:-
every objects have attributes
there are two types of attributes
mandatory and optional 

example:-
![[Pasted image 20230531184819.png]]
here kumar is object (user)
red: classes
Green: Attributes
Blue: values


### AD schema
Ad schema is a collection of classes and attributes
to get the schema you need to access ad schema file which is located at c:\windows\NTDS\ntds.dit
where ntds is new technolofy directory service directory information tree

#### Types of partition
+ Schema partition
+ Domain partition
+ Configuration Partition
+ Domain DNS Zone Partition
+ Forest DNS Zone Partition

#### Schema partition
This partition contains all classes and attributes

### Domain partition
Domain objects are stored in domain partition

### LDP
it is a tool based on LDAP which allows to view partitions of NTDS.DIT file

---
Types of Domain controller

### Root Domain controller:-
A first Domain Controller in the forest
it is also known as primary/Root DOmain controller

### Additional Domain controller:-
A type of Domain controller in the same domain.
It helps to share the load of RDC and provide fault tolerance
It always joins to an existing domain

ADC holds the replication of RDC 
![[Pasted image 20230531192014.png]]

problems in the above model

huge replication
This can be avoided by using child domain controller

### Child domain controller

A type of Domain controller which create a new child domain  
![[Pasted image 20230531193649.png]]
so after using child domain controller the schema appears like this 

Here we have 3 domains and 4 domain controller

### Tree domain controller
A type of Domain controller which create a new tree domain with new domain and domain dns partition
it always have unique domain name
it follows same schema with different Domain but with different names

### Read only domain controller
A domain controller which has read-only copy of ntds.dit file.

### Trees
collection of domains in the system is called tree
![[Pasted image 20230531200026.png]]


Forest:
collection of trees are called forests  and the forest is identified using root domain controller
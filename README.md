# Aurora Database
## Introduction 
AWS projects Aurora database service as the most suitable for enterprise-level database requirements. It is a MySQL- and PostgreSQL-compatible enterprise-class database, According to AWS:  
`Amazon Aurora supports up to 64TB of auto-scaling storage capacity, 6-way replication across three availability zones, and 15 low-latency read replicas.`  

## A. RDS Dashboard
Navigate to the RDS dashboard and launch the Create database wizard.  
![db1](db1.png?raw=true "db1")

## B. Create a Database
Once you launch the Create database wizard, you will be prompted with the following configuration details:

### 1. Database creation method
AWS provides two options to choose from:  
Standard create - You have set all of the configuration options, including ones for availability, security, backups, and maintenance.  
Easy create - You use the industry best-practice configurations. All configuration options, except the Encryption and VPC details, can be changed after the database is created.  
Choose the Standard create option.

![db2](db2.png?raw=true "db2")

### 2. Engine options
Choose Aurora with MySQL compatibility.
Select the Provisioned capacity and a default version.  

![db3](db3.png?raw=true "db3")

### 3. Templates
Use either the RDS Free Tier or Dev/Test template. On free-tier resources, you can develop and test applications to gain hands-on experience with Amazon RDS.  

### 4. Settings
Use the following values:
```
Field	                    Value
DB cluster identifier	    udacity-demo-db
Credentials Settings	    Provide a username and password of your choice
```
Take note of this password, as it is useful for future steps.  

![db4](db4.png?raw=true "db4")

### 5. DB instance size
Select the burstable classes (includes t classes).  
Include previous generation classes.  
Choose db.t2.small from the dropdown menu.  

### 6. Availability & durability
For production databases, use multiple AZs for reliability. If one AZ fails, the other one will still be available. It will create an Aurora Replica or Reader node in a different AZ.  

### 7. Connectivity
Use the following details:
```
Field	                        Value
Virtual private cloud (VPC)	    Choose the one available in your account
Subnet group	                Create a new subnet group (first-time)
Public. access	                No
VPC security group	            Choose existing default
```
![db5](db5.png?raw=true "db5")
![db6](db6.png?raw=true "db6")

### 8. Additional configuration
Use the following details:
```
Subsection	                Field	                Value
                        Database options	        Default
Backup	            Backup retention period	        1 day (default)
Encryption	        Enable encryption	            No
Backtrack	        Enable Backtrack	            No
Monitoring	        Enable Enhanced monitoring	    Yes
Log exports         None	
Maintenance	        Enable auto minor version upgrade	Yes
                    Maintenance window	            No preference
Deletion protection	Enable deletion protection	    Yes
```
![db7](db7.png?raw=true "db7")
![db8](db8.png?raw=true "db8")
![db9](db9.png?raw=true "db9")

### 9. Success message
You will be taken back to the dashboard, where you can see the details of the newly created database. 

![db10](db10.png?raw=true "db10")


Q: When should your database have a read replica?  
When you want to accommodate statistical reporting and other read-only queries  

## Using Cloudformation to Create DB
It is highly recommended to create your DB using the AWS console because db is a one time situation where u create the db. You don't want to be updating your Cloudformation script and having d db there.

Note that since setting up a database is usually a one-time event, you can just use the console (point and click) to create the database server instead of writing CloudFormation code. Using CloudFormation is still an option if you choose.  

### CloudFormation retention policy
You'll want your data to persist even if your stack of resources is updated or deleted.  
Retention Policy: keeps a service even if the entire stack of infrastructure is marked for removal. In CloudFormation, the syntax is DeletionPolicy: retain. This is very useful to assign to your data storage (database, file storage), to make sure that your data is saved even when the stack is updated or deleted.  


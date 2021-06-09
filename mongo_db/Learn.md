security:
  authorization: enabled

  Shutting down the server:

mongo admin --port 27001 --eval 'db.shutdownServer()'

Restarting the server with mongod.conf:

mongod -f mongod.conf


Connecting to MongoDB on port 27001:

mongo --port 27001


Running a find() query on the accounts database:

db.accounts.find( {}, { name: 1, ssn: 1 } )


---------

cat ~/workspace/mongod.conf

--------


Printing out the configuration file:

cat ~/workspace/mongod.conf

Connecting to MongoDB:

mongo --host localhost:27001

Retrieving all users:

db.getUsers()

Switching to the admin database:

use admin

Creating the user administrator:

db.createUser({
  user: "globalAdminUser",
  pwd: "5xd49$4%0bef#6c&b*d",
  roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
});

Authenticating as the user administrator:

db.auth( "globalUserAdmin", "5xd49$4%0bef#6c&b*d" )

Creating a cluster administrator:

db.createUser({
  user: "clusterAdminAny",
  pwd: "a*0f7@2c6#b4f%$d6c^c7d",
  roles: [ "clusterAdmin" ]
});


<!-- restarting mongo db with new configuration -->

Printing out the configuration file:

cat ~/workspace/mongod.conf

Connecting to MongoDB:

mongo --host localhost:27001

Retrieving all users:

db.getUsers()

Switching to the admin database:

use admin

Creating the user administrator:

db.createUser({
  user: "globalAdminUser",
  pwd: "5xd49$4%0bef#6c&b*d",
  roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
});

Authenticating as the user administrator:

db.auth( "globalUserAdmin", "5xd49$4%0bef#6c&b*d" )

Creating a cluster administrator:

db.createUser({
  user: "clusterAdminAny",
  pwd: "a*0f7@2c6#b4f%$d6c^c7d",
  roles: [ "clusterAdmin" ]
});


<!-- role based access control -->
If you want to learn about the roles that are only available from admin, visit the All-Database roles.

Creating a global user administrator:

use admin
db.createUser({
  user: "globalAdminUser",
  pwd: "5xd49$4%0bef#6c&b*d",
  roles: [ {
    role: "userAdminAnyDatabase",
    db: "admin"
  } ]
});

Creating a user administrator on the inventory database:

use admin
db.createUser({
  user: "inventoryAdminUser",
  pwd: "f46*5$2a3%ac&43f@17b",
  roles: [
    { role: "userAdmin", db: "inventory" }
  ]
});

Creating a user without any privileges:

use admin
db.createUser({
  user: "inventoryAdminUser",
  pwd: "4lf12$@0af0e4*9#8af",
  roles: [ ]
});

Granting a user the userAdmin privilege on the inventory database:

db.grantRolesToUser(
   "inventoryAdminUser",
   [ { role: "userAdmin", db: "inventory" } ]
)
          <!--Chapter 2: Role-Based Access Control  -->
Learning Activity: Granting Roles

Problem:

In the IDE below, there is a MongoDB instance with the following users already created for you on the admin database:

{
  user: "globalAdminUser",
  pwd: "5xd49$4%0bef#6c&b*d",
  roles: [ "userAdminAnyDatabase" ]
}

{
  user: "emailsAdmin",
  pwd: "70$5e%405*1fd87!47",
  roles: [ ]
}

{
  user: "emailReportsUser",
  pwd: "37f!98e1*c5%36&f4c",
  roles: [ ]
}

Please complete the following tasks:

    Grant the dbAdmin role on the emails database to emailsAdmin.
        This role will allow the emailsAdmin to perform administrative tasks on the emails database, such as schema-related tasks, indexing, and gathering statistics.
    Grant the readWrite role on the emails database to emailsAdmin.
        This role will allow the emailsAdmin to read and write all data on the emails database.
    Grant the read role on the emailReports database to emailReportsUser.
        This role will allow the emailReportsUser to read all data on the emailReports database.

You will need to authenticate as globalAdminUser in order to grant roles to other users.

You can connect to MongoDB and authenticate as globalAdminUser using this command:

mongo admin --port 27000 --username 'globalAdminUser' --password '5xd49$4%0bef#6c&b*d'
<!-- User defined roles  -->

If you want to learn about the operations associated with a specific privilege action, visit the Privilege Actions docs page.

Connecting to MongoDB on port 27001:

mongo admin --port 27001

Authenticating as the user administrator:

db.auth("globalAdminUser", "5xd49$4%0bef#6c&b*d")

Creating a new role grantRevokeRolesAnyDatabase:

db.createRole(
 {
   role: "grantRevokeRolesAnyDatabase",
   privileges: [
     {
        resource: { db: "", collection: "" },
        actions: [ "grantRole", "revokeRole", "viewRole" ]
     }
   ]
 }
)

Retrieving all roles:

db.getRoles()



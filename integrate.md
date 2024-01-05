# Flask REST API Integrate with keycloak 

### Prerequisite

Distributor ID:	Ubuntu  
Description: Ubuntu 22.04.3 LTS   
Release:	22.04  
Codename:	jammy  

1. Podman 
> podman version 3.4.4

2. python (Atleast)
> Python 3.10.12

3. Flask (Python Framework)
> Flask 2.3.3




### What is APIs? 

 API stands for Application Programming Interface. Imagine you're in a restaurant. You, as a customer, don't go into the kitchen and cook your food; instead, you interact with the waiter/waitress. You tell the waiter what you want to order, and the waiter takes that order to the kitchen, communicates with the chef, and brings back your food.

 Similarly, an API is like a waiter/waitress in a restaurant. It's a set of rules and protocols that allows different software applications to communicate and interact with each other. It defines how different software components should interact. It's like an intermediary that takes requests from one software (like your application) and communicates those requests to another software (like a server or database). Then it brings back the response to the requester.

 In the digital world, APIs allow different software systems, services, or platforms to talk to each other, exchange data, request services, or perform specific actions. They define the functionalities that developers can use in their applications without needing to know how those functionalities are implemented.


### What s Rest Api?

 REST API, which stands for Representational State Transfer Application Programming Interface, is an architectural style for designing networked applications. 

Key Concepts:  

- Resources: In a RESTful API, resources are the key abstraction. They represent any information that can be named and addressed. Resources are typically identified by URIs (Uniform Resource Identifiers).

- HTTP Verbs (CRUD operations): RESTful APIs use HTTP methods to perform actions on resources:

1. GET: Retrieve a resource or a collection of resources.
2. POST: Create a new resource.
3. PUT or PATCH: Update an existing resource.
4. DELETE: Remove a resource.

- Representation: Resources are represented in different formats like JSON, XML, HTML, or others, and clients can request specific representations of resources.


### Create Basic REST API using flask python language.

Ubuntu 22.04 comes with Python pre-installed. To install pip, you can use the following command:
```
sudo apt install python3-pip
```

How to install flask in ubuntu 22.04
```
pip install flask 
```
How to check flask --version
### Command -
```
flask --version
```

#### A Minimal Application-

I will create a basic RESTful API in Python using Flask framework and provide endpoints for creating users, getting all users

```
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello_world():
    return "<p>Hello, World!</p>"
```

Save it as hello.py or something similar. Make sure to not call your application flask.py because this would conflict with Flask itself.

To run the application, use the flask command or python -m flask. You need to tell the Flask where your application is with the --app option.

```
flask --app hello run
```
 and 
```
Flask run
```

After creataing basic Rest Api we integrate keycloak with Rest api come to the linux terminal and create directory ,`keycloak1`.

## First Step -

1. Creating a New Folder keycloak1

2. After Creating a keycloak1 folder > Right Click and Click on the 'Open with Other Application' > Click the Visual Studio Code.

> Creating a virtual environment (venv) with Vs code Terminal

Creating a virtual environment (venv) for a Python Flask project is a good practice as it helps isolate dependencies for your project and keeps your project environment separate from the system-wide Python installation.

### Command - 
#### Syntax
> python3 -m venv <Your_Venv_name>
```
python3 -m venv venv
```
#### Activate the Virtual Environment:
#### Syntax
> source <Your_Venv_name>/bin/activate

#### Command-
```
Source venv/bin/activate
```
Or
```
. venv/bin/activate
```

#### Output-
```
deepak@deepak-Inspiron-3502:~/keycloak1$ source /home/deepak/keycloak1/venv/bin/activate
(venv) deepak@deepak-Inspiron-3502:~/keycloak1$
```

Ubuntu 22.04 comes with Python pre-installed. To install pip, you can use the following command:
```
sudo apt install python3-pip
```

How to install flask in ubuntu 22.04
```
pip install flask 
```
How to check flask --version
### Command -
```
flask --version
```
4. Keycloak
```   
pip install keycloak
```
```
pip install Flask-OIDC
```

### How connect python flask Rest api with keycloak
## Second Step :

Keycloak:    Open Source Identity, Access Management, authentication to applications and secure services with minimum effort.
No need to deal with storing users or authenticating users.  
Keycloak provides user federation, strong authentication, user management, fine-grained authorization.

Install  keycloak....

## [Keycloak](https://www.keycloak.org/):

> Visit the Keycloak download page: [Keycloak Downloads](https://www.keycloak.org/downloads).   
> Click to TAR.GZ(sha1) and Download keycloak.
 
### After installation keycloak TAR.GZ(sha1) file unzip this file 
Go, files > Download > right click (on keycloak TAR.GZ(sha1) file and) > click Exteact Here.

## Get started with Keycloak Server on Podman  
Open the linux terminal -
## [Podman](https://docs.podman.io/en/latest/):
   Podman is a tool used to create, manage, and run containers. It allows users to package applications and their dependencies into isolated environments, making it easier to develop, deploy, and manage software.
   
## Podman install

### Command-
```
sudo apt-get update
```
### Output-
```
deepak@deepak-Inspiron-3502:~$ sudo apt-get update
[sudo] password for deepak: 
Hit:1 http://packages.microsoft.com/repos/code stable InRelease
Ign:2 https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/4.4 InRelease      
Ign:3 https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 InRelease      
Hit:4 https://download.docker.com/linux/ubuntu jammy InRelease                 
Hit:5 https://dl.google.com/linux/chrome/deb stable InRelease                  
Hit:6 https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/4.4 Release        
Hit:7 http://in.archive.ubuntu.com/ubuntu jammy InRelease                      
Hit:8 https://ppa.launchpadcontent.net/deadsnakes/ppa/ubuntu jammy InRelease   
Get:10 http://in.archive.ubuntu.com/ubuntu jammy-updates InRelease [119 kB]    
Get:11 http://security.ubuntu.com/ubuntu jammy-security InRelease [110 kB]     
Hit:12 https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/5.0 Release       
Hit:13 https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/jammy pgadmin4 InRelease
Hit:15 https://apt.postgresql.org/pub/repos/apt jammy-pgdg InRelease           
Get:16 http://ppa.launchpad.net/tektoncd/cli/ubuntu eoan InRelease [15.9 kB]   
Hit:17 http://in.archive.ubuntu.com/ubuntu jammy-backports InRelease
  The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 3EFE0E0A2F2F60AA
Reading package lists... Done
W: https://repo.mongodb.org/apt/ubuntu/dists/jammy/mongodb-org/4.4/Release.gpg: Key is stored in legacy trusted.gpg keyring (/etc/apt/trusted.gpg), see the DEPRECATION section in apt-key(8) for details.
W: https://repo.mongodb.org/apt/ubuntu/dists/focal/mongodb-org/5.0/Release.gpg: Key is stored in legacy trusted.gpg keyring (/etc/apt/trusted.gpg), see the DEPRECATION section in apt-key(8) for details.
N: Skipping acquire of configured file 'main/binary-i386/Packages' as repository 'https://apt.postgresql.org/pub/repos/apt jammy-pgdg InRelease' doesn't support architecture 'i386'
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.
```

## Command -
```
sudo apt-get upgrade
```
## output-
```
deepak@deepak-Inspiron-3502:~$ sudo apt-get upgrade
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Calculating upgrade... Done
The following packages were automatically installed and are no longer required:
  gir1.2-totem-1.0 gir1.2-totemplparser-1.0 libcdio-cdda2 libcdio-paranoia2
  libcdio19 libnetplan0 libnfs13 librsync2
Use 'sudo apt autoremove' to remove them.
The following packages have been kept back:
  python3-update-manager update-manager update-manager-core
0 upgraded, 0 newly installed, 0 to remove and 3 not upgraded.
```
## Command -
```  
sudo apt install podman
```
## output-
```
deepak@deepak-Inspiron-3502:~$ sudo apt install podman
[sudo] password for deepak: 
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
podman is already the newest version (3.4.4+ds1-1ubuntu1.22.04.2).
The following packages were automatically installed and are no longer required:
  gir1.2-totem-1.0 gir1.2-totemplparser-1.0 libcdio-cdda2 libcdio-paranoia2
  libcdio19 libnetplan0 libnfs13 librsync2
Use 'sudo apt autoremove' to remove them.
0 upgraded, 0 newly installed, 0 to remove and 3 not upgraded.
```
I'm already install podman ,so I got this output. If you don't have podman so it will be installed.

## Command- 
```
podman -v
```
## Output- 
```
podman version 3.4.4
```
Then Install keylock Pull the keycloak iamges using podman 

```
podman pull quay.io/keycloak/keycloak
```

## Second Step : 

Create a keycloak container using podman 

### Command:

```
podman run -p 8081:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:23.0.3 start-dev
```

### Output-
```
deepak@deepak-Inspiron-3502:~$ podman run -p 8081:8080 -e KEYCLOAK_ADMIN=admin -e KEYCLOAK_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:23.0.3 start-dev
Updating the configuration and installing your custom providers, if any. Please wait.
2023-12-23 06:05:25,250 INFO  [io.quarkus.deployment.QuarkusAugmentor] (main) Quarkus augmentation completed in 13127ms
2023-12-23 06:05:27,615 INFO  [org.keycloak.quarkus.runtime.hostname.DefaultHostnameProvider] (main) Hostname settings: Base URL: <unset>, Hostname: <request>, Strict HTTPS: false, Path: <request>, Strict BackChannel: false, Admin URL: <unset>, Admin: <request>, Port: -1, Proxied: false
2023-12-23 06:05:30,504 WARN  [io.quarkus.agroal.runtime.DataSources] (main) Datasource <default> enables XA but transaction recovery is not enabled. Please enable transaction recovery by setting quarkus.transaction-manager.enable-recovery=true, otherwise data may be lost if the application is terminated abruptly
2023-12-23 06:05:31,359 WARN  [org.infinispan.PERSISTENCE] (keycloak-cache-init) ISPN000554: jboss-marshalling is deprecated and planned for removal
2023-12-23 06:05:31,596 WARN  [org.infinispan.CONFIG] (keycloak-cache-init) ISPN000569: Unable to persist Infinispan internal caches as no global state enabled
2023-12-23 06:05:31,766 INFO  [org.infinispan.CONTAINER] (keycloak-cache-init) ISPN000556: Starting user marshaller 'org.infinispan.jboss.marshalling.core.JBossUserMarshaller'
2023-12-23 06:05:39,598 INFO  [org.keycloak.quarkus.runtime.storage.legacy.liquibase.QuarkusJpaUpdaterProvider] (main) Initializing database schema. Using changelog META-INF/jpa-changelog-master.xml

UPDATE SUMMARY
Run:                        117
Previously run:               0
Filtered out:                 0
-------------------------------
Total change sets:          117

2023-12-23 06:05:47,731 INFO  [org.keycloak.connections.infinispan.DefaultInfinispanConnectionProviderFactory] (main) Node name: node_15327, Site name: null
2023-12-23 06:05:47,913 INFO  [org.keycloak.broker.provider.AbstractIdentityProviderMapper] (main) Registering class org.keycloak.broker.provider.mappersync.ConfigSyncEventListener
2023-12-23 06:05:47,993 INFO  [org.keycloak.services] (main) KC-SERVICES0050: Initializing master realm
2023-12-23 06:05:51,625 INFO  [io.quarkus] (main) Keycloak 23.0.3 on JVM (powered by Quarkus 3.2.9.Final) started in 26.133s. Listening on: http://0.0.0.0:8080
2023-12-23 06:05:51,626 INFO  [io.quarkus] (main) Profile dev activated. 
2023-12-23 06:05:51,626 INFO  [io.quarkus] (main) Installed features: [agroal, cdi, hibernate-orm, jdbc-h2, jdbc-mariadb, jdbc-mssql, jdbc-mysql, jdbc-oracle, jdbc-postgresql, keycloak, logging-gelf, micrometer, narayana-jta, reactive-routes, resteasy-reactive, resteasy-reactive-jackson, smallrye-context-propagation, smallrye-health, vertx]
2023-12-23 06:05:52,267 INFO  [org.keycloak.services] (main) KC-SERVICES0009: Added user 'admin' to realm 'master'
2023-12-23 06:05:52,275 WARN  [org.keycloak.quarkus.runtime.KeycloakMain] (main) Running the server in development mode. DO NOT use this configuration in production.
^C2023-12-23 06:06:21,618 INFO  [io.quarkus] (Shutdown thread) Keycloak stopped in 0.087s

```
Then - 
```
Open the next Terminal 
```

After create podman container check podman container in your system 

### Command:
```
podman ps -a 
```

### Output: 

```
CONTAINER ID  IMAGE                               COMMAND     CREATED      STATUS                     PORTS                                           NAMES
cab3aded9c0f  quay.io/keycloak/keycloak:23.0.3    start-dev   5 days ago   Up 17 hours ago            0.0.0.0:8081->8080/tcp                          boring_euler

```

if your podman status not up so please run podman Container  

### command-

#### Syntax-

podman start <podman_container_names>

```
podman start 82148
```
or
```
podman start --latest
```

From a terminal, enter the following command to start Keycloak:-

> This command starts Keycloak exposed on the local port 8081 and creates an initial admin user with the username admin and password admin.

I execute this command then i am go browser and write `localhost:8081`(localhost:port)


## Third Step-

## ![image](https://github.com/Devendra-Singh6464/Flask_Rest_Api_Integrate_with_keycloak/assets/136952464/7b4abef4-f03c-4918-8745-57c3d12b5727)

Click Administration console  
## [Welcome to Keycloak page]![image](https://github.com/Devendra-Singh6464/Flask_Rest_Api_Integrate_with_keycloak/assets/136952464/2aa702a9-80f3-406b-931b-4dbd35dd5749)
:

Click on `Administrations Console`
 
Then i am go sign in page
>
  - username - `admin`  
  - password - `admin` 
> 

# Create a realm

A realm in Keycloak is equivalent to a tenant. Each realm allows an administrator to create isolated groups of applications and users. Initially, Keycloak includes a single realm, called master. Use this realm only for managing Keycloak and not for managing any applications.

## Use these steps to create the first realm.
>
1. Open the Keycloak Admin Console.  
2. Click the word master in the top-left corner, then click Create Realm.  
3. Enter `flask_app` in the Realm name field.  
4. Click Create.
>

## Create a user  
Initially, the realm has no users. Use these steps to create a user:
1. Open the Keycloak Admin Console.
2. Click the word master in the top-left corner, then click flask_app.
3. Click Users in the left-hand menu.
4. Click Add user.
5. Fill in the form with the following values:
   -  Email: `any email id`
   -  Email verified : `On`
   -  Users name: `any name`
   -  First name: `any first name`
   -  Last name: `any last name`
7. Click Create.

This user needs a password to log in. To set the initial password:
1. Click Credentials at the top of the page.
2. Fill in the Set password form with a password.
3. Toggle Temporary to Off so that the user does not need to update this password at the first login.

## Log in to the Account Console
You can now log in to the Account Console to verify this user is configured correctly.
1. Open the Keycloak Account Console.
2. Log in with Deepak and the password you created earlier.


   As a user in the Account Console, you can manage your account including modifying your profile, adding two-factor authentication, and including identity provider a


## Secure the first application
To secure the first application, you start by registering the application with your Keycloak instance:

1. Open the Keycloak Admin Console.
2. Click the word master in the top-left corner, then click flask_app.
3. Click Clients.
4. Click Create client
5. Fill in the form with the following values:
   -  Name: `OpenID Connect`
   -  Client ID:   `rest_api`
   -  Root URL: `http://127.0.0.1:5000/`
   -  Valid redirect URIs:`http://127.0.0.1:5000/*` 
   -  Admin URL :`http://127.0.0.1:5000/` Forth Step -

1. Creating a New Folder keycloak1

2. After Creating a keycloak1 folder > Right Click and Click on the 'Open with Other Application' > Click the Visual Studio Code.

> Creating a virtual environment (venv) with Vs code Terminal

Creating a virtual environment (venv) for a Python Flask project is a good practice as it helps isolate dependencies for your project and keeps your project environment separate from the system-wide Python installation.0/`
   -  Client authentication: `On`
   -  Authorization :`On`
      Logout settings : 
   -  Front channel logout: `On`
6. Click Next
7. Confirm that Standard flow is enabled.
8. Click Next.
9. Click Save.

> How to find our openid-configuration like- `issuer`,`auth_uri`,`userinfo_uri`,`token_uri`,`token_introspection_uri`
 1. Open the Keycloak Admin Console.
 2. Click the word master in the top-left corner, then click `flask_app`.
 3. Click `Realm settings` in the left-hand menu.
 4. Scroll Down and Click `OpenID Endpoint Configuration` link 

> How to find `Client Secret`-
 1. Open the Keycloak Admin Console.
 2. Click the word master in the top-left corner, then click `flask_app`.
 3. Click `Clients` in the left-hand menu.
 4. Click `rest_api`
 5. Click `Credentials` 


## Forth Step -

1. Creating a New Folder keycloak1

2. After Creating a keycloak1 folder > Right Click and Click on the 'Open with Other Application' > Click the Visual Studio Code.

> Creating a virtual environment (venv) with Vs code Terminal

Creating a virtual environment (venv) for a Python Flask project is a good practice as it helps isolate dependencies for your project and keeps your project environment separate from the system-wide Python installation.


Create a app.py file in keycloak1 Folder then run this command 
> app.py
```
import json
import logging
import os

from flask import Flask, g
from flask_oidc import OpenIDConnect
import requests
from keycloak import KeycloakOpenID
from oauth2client.client import OAuth2Credentials

logging.basicConfig(level=logging.DEBUG)

app = Flask(__name__)
app.config.update({
    'SECRET_KEY': 'TpuAEMd2qWVwfNsM6TevLOGmaljrgPeQ',
    'TESTING': True,
    'DEBUG': True,
    'OIDC_CLIENT_SECRETS': 'auth.json',
    'OIDC_ID_TOKEN_COOKIE_SECURE': False,
    # 'OIDC_REQUIRE_VERIFIED_EMAIL': False,
    # 'OIDC_EMAIL_VERIFICATION' = 'mandatory',
    'OIDC_USER_INFO_ENABLED': True,
    'OIDC_OPENID_REALM': 'flask_app',
    'OIDC_SCOPES': ['openid', 'email', 'profile'],
    'OIDC_TOKEN_TYPE_HINT': 'access_token',
    'OIDC_INTROSPECTION_AUTH_METHOD': 'client_secret_post'
    # 'OIDC_INTROSPECTION_AUTH_METHOD': 'bearer'
})

print(os.listdir())
os.chdir("/home/deepak/keycloak1")

oidc = OpenIDConnect(app)

keycloak_openid = KeycloakOpenID(server_url="http://localhost:8081/",
                                 client_id="rest_api",
                                 realm_name="flask_app",
                                 client_secret_key="TpuAEMd2qWVwfNsM6TevLOGmaljrgPeQ")

@app.route('/')
@oidc.require_login
def protected():
    info = oidc.user_getinfo(['preferred_username', 'email', 'sub'])
    username = info.get('preferred_username')
    email = info.get('email')
    sub = info.get('sub')
    print("""user: %s, email:%s"""%(username, email))

    token = oidc.get_access_token()
    return ("""%s"""%token)


@app.route('/private', methods=['POST'])
@oidc.accept_token(require_token=True)
def hello_api():
    return("""user: %s, email:%s"""%(g.oidc_token_info['username'], g.oidc_token_info['preferred_username']))


@app.route('/logout')
def logout():
    """Performs local logout by removing the session cookie."""
    refresh_token = oidc.get_refresh_token()
    oidc.logout()
    if refresh_token is not None:
        keycloak_openid.logout(refresh_token)
    oidc.logout()
    g.oidc_id_token = None
    return 'Hi, you have been logged out! <a href="/">Return</a>'


if __name__ == '__main__':
    app.run()
```

After Creating app.py ,then Create a auth.json File in same folder
> auth.json
```
{
    "web": {
      "issuer": "http://localhost:8081/realms/flask_app",
      "auth_uri":  "http://localhost:8081/realms/flask_app/protocol/openid-connect/auth",
      "client_id": "rest_api",
      "client_secret": "TpuAEMd2qWVwfNsM6TevLOGmaljrgPeQ",
      "redirect_uris": [
        "http://localhost:5000/*"
      ],
      "userinfo_uri": "http://localhost:8081/realms/flask_app/protocol/openid-connect/userinfo",
      "token_uri":"http://localhost:8081/realms/flask_app/protocol/openid-connect/token",
      "token_introspection_uri":"http://localhost:8081/realms/flask_app/protocol/openid-connect/token/introspect",
      "bearer_only": "true"
    }
  }
```

> How to find our auth file-  `issuer`,`auth_uri`,`userinfo_uri`,`token_uri`,`token_introspection_uri`
 1. Open the Keycloak Admin Console.
 2. Click the word master in the top-left corner, then click `flask_app`.
 3. Click `Realm settings` in the left-hand menu.

> How to find `Client Secret`-
 1. Open the Keycloak Admin Console.
 2. Click the word master in the top-left corner, then click `flask_app`.
 3. Click `Clients` in the left-hand menu.
 4. Click `rest_api`
 5. Click `Credentials` 

Then you go vs code terminal and again run over flask app-

```
flask run
```
And you click and open `127.0.0.1:5000`

#### Output :
(venv) deepak@deepak-Inspiron-3502:~/keycloak1$ flask run
['requirements.txt', 'Screenshot from 2023-12-28 13-36-02.png', 'auth.json', 'app.py', '__pycache__', 'integrate.md', 'Screenshot from 2023-11-18 17-12-07.png', 'venv']
DEBUG:urllib3.util.retry:Converted retries value: 1 -> Retry(total=1, connect=None, read=None, redirect=None, status=None)
DEBUG:urllib3.util.retry:Converted retries value: 1 -> Retry(total=1, connect=None, read=None, redirect=None, status=None)
 * Debug mode: off
INFO:werkzeug:WARNING: This is a development server. Do not use it in a production deployment. Use a production WSGI server instead.
 * Running on http://127.0.0.1:5000
INFO:werkzeug:Press CTRL+C to quit

If the link is opened,a login page will open in front of you in which you will have to enter you email or password and then 1 token will come to your front then go to your Vs code terminal or your will see that your data will be visible on vs code terminal.



 

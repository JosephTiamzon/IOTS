<h1>SMART DOOR LOCK (IOTS PROJECT)</h1>

|  Name |  Admission ID  |
|  -------------  |  -------------  |
|  Leong Ming Liang Timothy  |  P1907799  |
|  Ron Tan Zi Yu |  P1908521  |
|  Tiamzon Joseph Martin |  P1907492  |

<h3>Concept</h3>
The user will use a keypad to enter a code to unlock the door. It also uses an LCD to give prompts to the user. Users will also be able to configure their device information through a website.
</br>

<h3>Components</h3>
<ul>
  <li>Hardware
    <ul>
      <li>Esp32</li>
      <li>4x4 Keypad</li>
      <li>I2C LCD 16x2 with PCF8574 IIC I2C Serial Interface Adapter</li>
      <li>SG90 Servo Motor</li>
      <li>12x Female-to-Male Jumper Wires</li>
      <li>3x Male-to-Male Jumper Wires</li>
      <li>Breadboard</li>
    </ul>
  </li>
  <li>Website
    <ul>
      <li>NextJS</li>
      <li>ReactJS</li>
      <li>Auth0</li>
      <li>Vercel</li>
    </ul>
  </li>
  <li>Database
    <ul>
      <li>Mongodb</li>
    </ul>
  </li>
</ul>
<h3>How users are meant to operate and use the product</h3>
<h5>Setting up on the website</h5>
Users will need to set up their device to be connected to the database. To do that, the first thing a user will need to do is to register an account through the website. https://iots.vercel.app/ . After they signed in, they will click create a new device. They fill in the form then press create. Take not of the device id as you will need it later. You can create, read, update and delete your devices through the website.

<h5>Setting up on the door lock</h5>
After the user has created a new device in the website, they will go to the door lock and turn it on. After the door lock boots up, they will be prompted to add in the device id they got earlier on. 
</br>
</br>
Thats it! Your smart door is ready to work

<h3>TR64 Compliance Checklist</h3>

|  TR64 Category  |  Compliance Request ID  |
| ------------- | ------------- |
| Cryptographic Support  | CS-01, CS-02, CS-03, CS-04, CS-05  |
| Security Function Protection  | FP-01  |
| Identification & Authentication  | IA-01, IA-02, IA-03, IA-04  |
| Data Protection  | DP-02, DP-04  |
| Access Protection  | AP-01, AP-02, AP-05  |
| Security Management  |  MT-01, MT-02  |
| Resiliency Support  | RS-03, RS-04  |
| Security Audit  | AU-01, AU-02  |
| Lifecycle Protection  | LP-01, LP-02, LP-03, LP-05, LP-06, LP-07, LP-08, LP-09  |

<h3>Attack Surfaces</h3>
<h4>Attack Surface 1: Physical Attacks (ESP-32)</h4>
<h5>Vulnerabilities</h5>
<p>
Physically tampering with the door access system and injecting of external code into the microcontroller controlling the door system could potentially result in the whole system failing.
</p>
<h5>Assessment</h5>

|  Category  |  Description  |
|  --------  |  -----------  |
|  Damage  | An attack on the physical hardware would have a very high impact as the physical hardware is the core of the Door Access System.  |
|  Reproducability  | An attack on the hardware level would be very hard to reproduce as it would require the attacker to be physically present at the same location as the hardware  |
|  Exploitability  |   This attack would be considered as high exploitability since our hardware is not in the most secure position  |
|  Affected Users  |  The home owner would be the main affected user as it would compromise the entire security system, allowing anyone to enter the home of the home owner.  |
|  Discoverability  |  An attack at this level would be very high on the discoverability scale as this attack requires the home owner to be physically present at the site where the security system is, which in this case is the home.  |

<p align="center">
<img src="/img/OWaspVulnerabilityScore1.png" alt="Calculated Vulnerability Score 1" width="100%" height="100%">
</p>
CVSS:3.0/AV:P/AC:H/PR:H/UI:N/S:C/C:N/I:N/A:H

<h5>Mitigation</h5>
<p>
In order to mitigate this attack, physically securing the Door Access System with proper procedures would be recommended. In order to achieve this, we created a tamper proof enclosure for the ESP-32 microcontroller so that it would be very difficult for them to inject their own code and tamper with the microcontroller.
</p>



<h4>Attack Surface 2: ESP-32 Network Attack</h4>
<h5>Vulnerabilities</h5>
<p>
Intercepting of packets being sent from the "Door Access" terminal to the secure endpoint on MongoDB would result in the Personal Identifiable Information (PII/SPI) being leaked to the hacker as they would be able to know the specific time as to when the home owner leaves and returns.
</p>
<h5>Assessment</h5>
<p>

|  Category  |  Description  |
|  --------  |  -----------  |
|  Damage  | An attack at this level would be be very low risk as there are proper security procedures implemented into this. For example, packets are sent through using TLS, meaning that it is very hard for hackers to identify and decrypt the Personal Identifiabe Information.  |
|  Reproducability  |  In order to reproduce this type of attack, it would be very easy. However, the exploitaility of this attack is very low.  |
|  Exploitability  |  This attack has a low exploitability as the packets being sent over are encrypted using TLS.  |
|  Affected Users  |  Home Owners are the only users that would be affected.  |
|  Discoverability  |  Eavesdropping and sniffing are attacks which are very hard to discover.  |

<p align="center">
<img src="/img/OWaspVulnerabilityScore2.png" alt="Calculated Vulnerability Score 2" width="100%" height="100%">
</p>
CVSS:3.0/AV:N/AC:L/PR:N/UI:R/S:U/C:L/I:N/A:N 
</p>

<h5>Mitigation</h5>
<p>

</p>
<h4>Attack Surface 3: Database Attacks (MongoDB)</h4>
<h5>Vulnerabilities</h5>
<p>
Stealing access to administrator account.
</p>
<h5>Assessment</h5>

|  Category  |  Description  |
|  --------  |  -----------  |
|  Damage  | The damage would be high if the administrator account would be accessed by a threat actor. This is because the administrator has access to all data and is able to configure the server settings |
|  Reproducability  | the reproducability is high if the threat actor has found the credentials of the administrator account |
|  Exploitability  | The exploitability is low as the administrator account of our Mongodb database is securely protected using social login with 2 factor authentication and the password follows the standard of strong password. |
|  Affected Users  | All users would be affected as the administrator has access to all data and system configuration|
|  Discoverability  | The discovery of the threat would not be easy as we did not leave save our credentials insecurely |

<h5>Mitigation</h5>
<p>
The mitigation would be using social logins that is using 2 factor authentication, a strong password to the social login, limiting the amount of people having administrator rights and logging of important events. 
</p>
<h4>Attack Surface 4: Web Server Attacks (Vercel)</h4>
<h5>Vulnerabilities</h5>
<p>
DDoS of the Vercel webserver to take down availability. 
</p>
<h5>Assessment</h5>

|  Category  |  Description  |
|  --------  |  -----------  |
|  Damage  | The damage is medium as users will not be able to create, read, update and delete their door lock configuration.  |
|  Reproducability  |  It is not easy to take down Vercel webserver with DDoS as there are implementation to prevent this attack  |
|  Exploitability  |  To do DDoS of a scale that is able to take Vercel down, the threat actor would need to use a huge amount of zombies  |
|  Affected Users  |  All of our users would be affected if Vercel goes down  |
|  Discoverability  |  It is not easy to discover how to do a DDoS attack that works on Vercel |

<h5>Mitigation</h5>
<p>
The system needs to be able to detect a suspicious activities users and black list that IP address. 
</p>

<h4>Attack Surface 5: Web Application Attacks (Auth0)</h4>
<h5>Vulnerabilities</h5>
<p>
Brute force attack on a user in our website application
</p>
<h5>Assessment</h5>

|  Category  |  Description  |
|  --------  |  -----------  |
|  Damage  | The damage would be high if the threat actor is able to log in as another user  |
|  Reproducability  |  It is not easy to reproduce this attack as Auth0 has implementation against brute force attack |
|  Exploitability  |  It will require a lot of work to be able to brute force Auth0 authentication  |
|  Affected Users  |  Only the user being brute forced would be affected  |
|  Discoverability  |  It is easy to find tutorials on how to execute this attack  |

<h5>Mitigation</h5>
<p>
Auth0 already has mitigations to brute force attack. Auth0 will block suspicious IP addresss from logging in as that user and sends an email to the affected user.
</p>
</p>
<h3>Compliance Lists</h3>
<h4>Webpage Compliance List</h4> 
<i>TR64 Req IDs: CS-02;IA-01;RS-03;MT-02</i>

|  TR64 Req ID  |  Explanation  |
|  -------------  |  -------------  |
|  CS-02;IA-01  |  User created passwords for Auth0 are hashed using bcrypt.  |
|  RS-03  |  Web server is secured by vercel with security grade procedures. Able to withstand malicious threats such as Denial of Service (DoS) and Distributed Denial of Service (DDoS).  |
|  MT-02  |  Users are only able to create, read, update and delete their own data so to uphold confidentiality and that data will not be tampered by unauthorized users.  |

<h4>MongoDB Atlas Compliance List</h4>
<i>TR64 Req IDs: CS-01;CS-04;CS-05;FP-01;DP-04;RS-04;AU-01;AU-02;MT-02 </i></br>

|  TR64 Req ID  |  Explanation  |
|  -------------  |  -------------  |
|  CS-01  |  API keys are generated by Mongo.  |
|  CS-04  |  RS256 asymmetric encryption algorithm is used to sign Json Web Tokens (JWTs) for authentication to web application.  |
|  CS-05;FP-01  |  API Keys are created for trusted endpoints and are fully managed by MongoDB with industrial grade security features.  |
|  DP-04  |  Role based access is assigned for different users.  |
|  RS-04  |  MongoDB Atlas provides a tool that enables backups of the entire database to be created easily. The backup can be used for disaster recovery in the event of an IoT attack.  |
|  AU-01;AU-02  |  Audit log consists of all entries, including Create, Read, Update and Delete (CRUD) as well as any successful or unsuccessful authentications. Audit logs are also secured and tamper proof. Only the authorized user with the proper credentials/API key would be able  to access it.  |
|  MT-02  |  Role based access is granted to specific users such that there are no over privileged accounts, which poses as a IoT security vulnerability.  |

<h4>Auth0 Compliance List </h4>
<i>TR64 Req IDs: CS-05;MT-01;IA-01;IA-02;IA-03;IA-04;DP-02;AP-01;AP-02;AP-05</i> </br>

|  TR64 Req ID  |  Explanation  |
|  -------------  |  -------------  |
|  CS-05;IA-01  |  Passwords created for specific user accounts are hashed using bcrypt before being stored in the MongoDB to ensure <bold>confidentiality</bold> of user credentials.  |
|  IA-02  |  Authentication to web server has a set session expiry of 7 days before the user is prompted to sign in again.  |
|  IA-03  |  Unique tokens are generated and assigned to users using JWTs to guarantee the Authenticity of users.  |
|  IA-04;AP-02;MT-01  |  Users are required to create a complex password upon signing up. 2 factor authentication is also required for users who sign in using third-party applications such as Google or Microsoft Account.  |
|  DP-02  |  Digital signatures are created using RS256 to sign Json Web Tokens for <b>Non-Repudiation</b> and <b>Integrity</b>, making sure the content has not been tampered with.  |
|  AP-01  |  Failure to enter password consecutively would result in an account lockout followed by blocking of the suspected user IP Address. Account owner would also be notified of the suspicious activity and given a choice to unblock the IP Address.  |

<h4>ESP32</h4> 
<i>TR64 Compliance List: CS-02;IA-01</i> </br>

|  TR64 Req ID  |  Explanation  |
|  -------------  |  -------------  |
|  CS-02;IA-01:  |  We used a cryptographic algorithm (PBKDF2) to hash the device password with salt for better <b>confidentiality</b>.  |

<h3>Documentation</h3>
<h4>Website</h4>
The website is hosted on vercel and is reachable via https://iots.vercel.app/ . The website is built on NextJS which is a meta ReactJS framework which allows developers to create full stack web application. It also uses MongoDB as a database to store the user device information and Auth0 to handle user authentication and storing of user information.

<h5>To get started</h5>
<ol>
  <li>
  You will need to have nodejs installed. Go over to https://nodejs.org/en/ to install nodejs
  </li>
   <li>
  Clone this repository or download the zip file
  </li>
  <li>
  Open it up using visual studio code or equivalent and go to the root path of the dashboard which is /IOTS/IOTS-dashboard
  </li>
  <li>
  From here you can choose to either run it in localhost mode or push it to the cloud. 
  <br/>
  <b>If you want to push it to the cloud</b>
    <ol>
      <li>
      Create a new github repository and push the code to the repository
      </li>
      <li>
      Create a vercel account and link it to your github https://vercel.com/
      </li>
      <li>
      After signing in to vercel, go to add <b>new project</b>
      </li>
      <li>
      Import the repository that you created
      </li>
      <li>
      Select the NextJS under the <b>Framework Preset</b>
      </li>
      <li>
      Ensure that the <b>Root Directory is the root path of the website</b>
      </li>
      <li>
      Then click deploy
      </li>
      <li>
      All codes that are commited to github will be rebuilt and redeployed on vercel.
      </li>
    </ol>
    <b>If you want to run it locally using localhost</b>
      <ol>
      <li>
       Go to the root path of the website locally from your terminal in visual studio code or equivalent
      </li>
      <li>
       Type in npm run dev
      </li>
      <li>
       Open your browser and go to http://localhost:3000/
      </li>
      <li>
       You should see the website running
      </li>
      </ol>
    </li>
    <li>
    Now you need to create a new Auth0 account https://auth0.com/
    </li>
    <li>
    Login to auth0 
    </li>
    <li>
    Go to applications and create a new application
    </li>
    <li>
    Select Regular Web Application
    </li>
    <li>
    Take note of the <b>Client ID</b> and <b>Client Secret</b>
    </li>
    <li>
    Scroll down to <b>Allowed Callback URLs</b>
    </li>
    <li>
    Add in  https://YOUR-VERCEL-APP-URL/api/auth/callback/auth0, http://localhost:3000/api/auth/callback . You do not need to add in the first one if you did not push       the code to vercel
    </li>
    <li>
    Scroll down and save your changes
    </li>
    <li>
    Now you need to create your MongoDB database
    </li>
    <li>
    Head over to https://www.mongodb.com/ and create a new account
    </li>
    <li>
    Create a new project and name it IOTS
    </li>
    <li>
    Create a new cluster and select <b>shared</b> and change the cluster name to IOTS-database
    </li>
    <li>
    Go to browse collection of IOTS-database
    </li>
    <li>
    Go to collections tab and create a new database
    </li>
    <li>
    Go to collections tab and create a new database
    </li>
    <li>
    Name the <b>database name</b> as IOTS_dashboard and the <b>Collection name</b> as users
    </li>
    <li>
    Hover over IOTS_dashboard and create another collection and name it as users
    </li>
    <li>
    Go over to App Services
    </li>
    <li>
    Go to Authentication tab
    </li>
    <li>
    Click on edit for <b>Custom JWT Authentication</b> 
    </li>
    <li>
    Enable the provider and select <b>Use a JWK URI</b>
    </li>
    <li>
    Under <b>JWK URI</b> go back to auth0 application settings and scroll all the way down to advanced settings
    </li>
    <li>
    Go to the <b>Endpoints</b> tab and copy the JSON Web Key Set. It should look something like https://YOUR-TENANT/.well-known/jwks.json
    </li>
    <li>
    Go back to the MongoDB and paste what you copied to the JWK URI
    </li>
    <li>
    Go to trigger and add a new trigger
    </li>
    <li>
    Set the trigger type to Authentication
    </li>
    <li>
    Name the Trigger AddUserToDatabase
    </li>
    <li>
    Set your <b>Cluster name</b> to IOTS-database
    </li>
    <li>
    Set your <b>Database name</b> to IOTS-dashboard
    </li>
    <li>
    Set your <b>Collection name</b> to users
    </li>
    <li>
    Scroll down and click on <b>select a function</b> and create a new function
    </li>
    <li>
    Name the function addUserToDatabase
    </li>
    <li>
    Copy this code and place it in the function
    
```javascript
exports = function(authEvent) {
  const user = authEvent.user;
  const mongodb = context.services.get("IOTS-database");
  const usersCollection = mongodb.db("IOTS_dashboard").collection("users");
  usersCollection.insertOne({
    ...user
  });
};
```
</li>
    <li>
    Save it and go back to the <b>Authentication</b> tab
    </li>
    <li>
    Click on edit for the API Keys and create a new API Key and name it Door_Auth. Save the API key somewhere safe as you will not see it again. This will be your API key that you will use for the esp32 query
    </li>
    <li>
    While you are saving the api key, on the sidebar, at the top, there is a copy icon. Click on it as save it as that is your app id and you will need it later
    </li>
    go back to the auth0
    <li>
    Go over to APIs and create a new API
    </li>
    <li>
    Name it whatever you want and the identifier is the mongodb app id which you saved and the click create
    </li>
    <li>
    Now if you are running the code on localhost, create a <b>.env</b> file at the <b>root directory</b>. If you are using vercel go over to <b>settings</b> and <b>Environment Variables</b>. Then add this into your env either on vercel or your .env file in your root directory
    
```
AUTH0_CLIENT_ID = <Your auth0 application client ID>
AUTH0_CLIENT_SECRET = <Your auth0 application client secret>
AUTH0_ISSUER = https://<your auth0 application domain> 
NEXTAUTH_URL = <your website url either localhost or the vercel url>
NEXT_PUBLIC_APP_ID= <your mongodb app id that you saved>
AUTH0_AUDIENCE= <your mongodb app id that you saved>
NEXTAUTH_SECRET= <random secret of any length that you can use openssl to generate for you. would recommend 32 characters long>
NEXT_PUBLIC_SALT = <the salt that you will use to hash the users device password. would also recommend to use openssl and 32 characters long to generate the salt>
```
</li>
  <li>
    Go back to mongodb app services
  </li>
  <li>
    Go to HTTPS Endpoints and create a new HTTPS Endpoint 
  </li>
  <li>
    Set the route to be /doorauth
  </li>
   <li>
    Under <b>Operation Type</b> copy the url
  </li>
  <li>
    Set the <b>HTTP Method</b> to post
  </li>
  <li>
    Set the <b>Return Type</b> to JSON
  </li>
   <li>
    Under <b>Function</b> add a new function and copy this code
    
    
```javascript
exports = async function({ query, headers, body}, response) {
  const CryptoJS = require("crypto-js");

    const serialized = body.text();
    const data = JSON.parse(serialized);
    
    const {deviceId, userPassword} = data;
    console.log(deviceId);
    console.log(userPassword)
    const dbPassword = await context.services.get("IOTS-database").db("IOTS_dashboard").collection("iot").findOne(
    {device_id: deviceId},
    {password: 1}
    )
    console.log(dbPassword);
    
    console.log("dbpassword", dbPassword)
    
    if (dbPassword){
      console.log("not null")
       if (dbPassword.password === CryptoJS.PBKDF2(userPassword, "<Your salt that you generated just now>",  {
              keySize: 256 / 32,
              iterations: 1000,
            }).toString()){
              console.log("authorised")
         return "authorised"
       }
        return "Username or Password is invalid"
    }else{
      console.log('invalid')
      return "Username or Password is invalid";
    }

};

```
</li>
  <li>
  Go to your esp32 code and add the API key of the doorauth you saved just now as well as add your http endpoint url to the endpoint variable
  </li>
</ol>

<h5>Circuit Diagram</h5>
<p>The diagram below shows how the components are connected to create the circuit diagram. the tables shows the different pin connections to the Esp32 I/O pins.</p>
<p align="center">
<img src="/img/hardware_circuit_diagram.jpeg" alt="IOTS Circuit Diagram" width="70%" height="70%">
</p>

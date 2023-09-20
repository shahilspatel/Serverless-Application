<h1>Serverless Application</h1>


<h2>Description</h2>
Hosted a website using Amplify with HTML, CSS, Javascript, and image files which are loaded into the browser from an S3 bucket. JavaScript executed in the browser sends and receives data from a public backend API built using Lambda and API Gateway. Amazon Cognito provides user management and authentication functions to secure the backend API. DynamoDB provided a persistence layer where data can be stored by the API's Lambda function.


<h2>Languages and Utilities Used</h2>

- <b>AWS S3</b> 

- <b>AWS Cloudfront</b>

- <b>AWS Certificate Manager</b>

- <b>AWS Lambda</b>

- <b>DynamoDB</b>

- <b>Github Actions</b>

- <b>Terraform</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)

<h2>Program walk-through:</h2>

<h3>Hosting the Static Website</h3>

Initial AWS Configuration:  
Entered AWS credentials, removed due to access keys being shown. Code shown below:
<br />  
  
```
% aws configure
AWS Access Key ID [****************]: #####################
AWS Secret Access Key [****************]: ###################
Default region name [us-east-1]: us-east-1
Default output format [None]: 
```

- An AWS CodeComit repository was created called wildrydes-site that was going to be the location for the public S3 bucket to be copied to. We used the git clone command to bring the empty repository to our local machine.

- Due to the permission policy only granting permission to CodeCommit for the IAM Role being used for this project, AWS CodeCommit was necessary, in a future project Github can be implemented.

Cloning the Initial AWS CodeCommit Repository to Local Machine: <br/>
<img src="https://i.imgur.com/RpHU2tm.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- Using a public S3 bucket, we copied the static files by navigating to our directory with the cd command and the cp command to copy the files to our local machine.

- We then added, committed, and pushed our git files using their respective commands. 

The Git Push of the Public S3 Bucket:  <br/>
<img src="https://i.imgur.com/ZFzAxEo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- The Amplify Console is used to set up a place to store your static web application code and to simplify the lifecycle of that application. AWS Amplify was used to create a host the web application using the repository made in CodeCommit. The application is shown below:
  
The Wild Rydes Application Launch on Amplify:  <br/>
<img src="https://i.imgur.com/NROcBxP.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


<h3>Managing the User Pool with Amazon Cognito</h3>


- Using Amazon Cognito, we create an user pool to integrate with our web app. We updated our Javascript config file to have the relevant data from the user pool and Cognito. The new file is added, committed, and pushed to our repository.

Javascript Configuration File With Updates:  <br/>
<img src="https://i.imgur.com/yJ3geai.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

- After updating the repository, we opened the register.html file, and registered a second a verified SES email with account information to send a verification code to. The code was successfully sent to my second email through the register.html, we automatically moved to the the siginin.html, and then entered the verification code along to sign in. The next file 'ride.html' was not able to open as we not have not setup the API invoke url in our configuration file.


<h3>Serverless Service Backend</h3>

- We implemented a Lambda function that will be invoked each time a user requests a unicorn. The function will select a unicorn from the fleet, record the request in a DynamoDB table, and then respond to the frontend application with details about the unicorn being dispatched.

- After the DynamoDB table for 'Rides' was created, we created an IAM role for our Lambda function that granted it DynamoDB write permission.

- We created a Lambda function that use our role we created with a prewritten requestUnircon.js Javascript file and then tested it with a test event of inputting null data.

Test Event Success:  <br/>
<img src="https://i.imgur.com/k1XEGr7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>

<h3>Deploying a RESTful API</h3>

The static website  deployed in the first module already has a page configured to interact with the API that is to be built in this section. The page at /ride.html has a simple map-based interface for requesting a unicorn ride. After authenticating using the /signin.html page, the users will be able to select their pickup location by clicking a point on the map and then requesting a ride by choosing the "Request Unicorn" button in the upper right corner.

- Once the API is deployed using edge-optimized for the endpoint type, an Amazon Cognito User Pools Authorizer was created to authenicate the API's calls. After this, a resource was created within the API, then a POST method was created and it was configured to use Lambda proxy integration backed by the RequestUnicorn function.

- The API is then deployed and the config.js file was updated with the Invoke URL from the AP. The new config.js is added, committed, and pushed to the repository to automatically deploy in Amplify.

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>

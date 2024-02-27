# IDOR (Insecure Direct Object Reference)

<h2> What is Insecure Direct Object References Attack?</h2> <br>

An insecure direct object reference (IDOR) is an access control vulnerability where invalidated user input can be used for unauthorized access to resources or operations. It occurs when an attacker gains direct access by using user-supplied input to an object without authorization. Attackers can bypass the authorization mechanism to access resources in the system directly by exploiting this vulnerability. Every resource instance can be called an object and often, represented with an ID. And if these IDs are easy enough to guess or an attacker can use an object to bypass the access check somehow, we can talk about an IDOR at this point. Referring to the above image, an attacker by ethical means can only get the document numbered 101 which is legally his. But what if the web application does not validate the number and an attacker puts the number of its victim? This can cause the attacker to get hold of the sensitive document to which he should not have access. <br>

<h2> Severity: </h2><br>

The severity of IDOR varies from P3 to P2 depending on what data is being exposed.<br>

<h2> LAB 1: Give me my amount!!</h2>
Observation: <br>
On accessing the first lab of this module we can see the view hasn't changed much from that of previous labs, Now we can observe that we are given a login page with the name as, 'Bank Login Page', we can also see it has two identical buttons first for Login and later for Register as shown in the first image
<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/d99c2427-ad5e-4cfb-b214-d13cd762e4f9"><br><br>
On Clicking the 'Register' button we can observe the following interface to add a new user,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/c8d505f0-076b-431c-a72e-ab80d5eb78c9"><br><br>

Solution: <br>
IDORs are fun and have a good bounty!<br>
Now first things first let's go to the register page and make a user account. (email: abc@mail.com, Password: 123)<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/f11b8fa3-a336-4484-acc4-c8acf206fd9d"><br><br>
Let's log in to our user account, using the set credentials, and we can see,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/261c0684-4cc0-4d4a-8ed9-ebb4203c4881"><br><br>
The first thing we should know about coding a login page with multiple users is parameters should not be displayed and if displayed there should be checks such that these can't be tampered with. <br><br>
Now as in this URL as marked, we can see the "/profile.php?id=" id parameter, and that too has a numerical value telling us a lot about the backend architecture such as the database at the backend where user profiles are created would have following fields (id, Email, Password, Transaction 1, Transaction 2, Transaction 3), and my user is in the 66th row or is the 66th user. <br>
IDORs are particularly simple we just need to test over these open parameters for the unauthorized information disclosure of other users.<br>
Let's try changing the id value from "id=66" to "id=65", and we can observe<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/0215e6a6-92b2-4124-b586-e0082066db74"><br><br>
And by this, we know our current lab site is vulnerable to IDOR vulnerability.<br>
Before we move on to the next lab let's see if can we get the details of all users.<br>
Let's turn up our Swiss army knife and use it for our testing.<br><br>
First like in the past we'll intercept this request when the browser is requesting for the user with some '?id=', <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/3e23c537-e2c0-4c36-af9c-0984e86833eb"><br><br>
Now send the following request to burp intruder, and click on the clear all button then select the value '65' and click the add button, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/8efc2c6c-496b-4541-a1c1-20f86c36325d"><br><br>
Now select attack type as 'Sniper' and in the payloads, option select 'Numbers', as shown,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/42f08c68-5a7e-4bae-bb8f-b3dc977adb29"><br><br>
Hit the 'Start Attack' button, and analyze each response you got<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/825c9372-2a6d-4f7d-97e0-fd73b255ded6"><br><br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/d49485cb-d692-4666-952a-930b14c73540"><br><br>

Now as we can see when we log in to our account we can also update our details, by far we know that we have the read access privilege to read the contents of the profiles of others, which is serious enough when we take into account that it's a bank application. To increase the impact of the existing vulnerability let's also test whether we can update other accounts or not.<br>
This is just the profile of 'id=33'<br>

<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/1f019d3a-9047-40db-b4e3-a0d5d5fef0ed"><br><br>

Now let's play with the input fields, like,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/2fea6174-32cf-4ef1-9ca6-f2148f467a86"><br><br>
Hit Update!<br>
Log out!<br>
Log in again! <br>
Navigate to the same id (in my case id=33), and check for yourself.<br>
<br>
After this we can suspect that this application has a common database for all so try and share a screenshot of the user with id = 33 of what you see (over Whatsapp or Discord). <br> 


<h2> LAB 2: Stop polluting my params!</h2>
Observation: <br>
Upon accessing the lab we are thrown a login page with the fields asking for Email and Password combination, we also have two buttons each for login and Register.<br>

<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/a1e3bfc0-d836-4cf4-9ea7-1d42e6c088b5"><br><br>
Upon clicking the Register button we are given a page as follows,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/951df9d8-076b-4739-96d1-1c81b1b42fe8"><br><br>

Solution:<br>
As from the last lab, we know how an IDOR vulnerability works, let's just create a new user account and see what more can we do with it...:)
<br>
So using some random details to create the account such as,<br/>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/54461bb3-ab7b-4f05-889f-66e161d4944a"><br><br>
Here, we have email: password => something@mail.co: 123 <br>
Now we'll just register this user and log in with our credentials,<br>
When we log in, we get the following response for our 'User Profile',
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/97f5d183-7e4f-4cf7-81b5-6cc859a23b2a"><br><br>
As we did in the previous lab, let's try changing the value of the '?id=" parameter, we get,<br>
We changed our value to 20,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/6a606468-adaa-4b7e-9d7b-7aeab7d1b09e"><br><br>
This is similar to what we did in the last lab and here in this lab we were not allowed to update the accounts of other users too...<br>
So same for 2 labs doesn't seem right to me!! Also as we practiced that during challenges, labs, or Ctfs the biggest hint is the name for the one...<br><br>
So after reading the name, this was one of the findings that the majority of the people left, now a question can we launch our IDOR in some other way??<br><br>
The answer to this is yes, what if this is a real-world scenario and you are not getting the accounts of other users, would you just give up? The lab says, "Don't pollute my parameters." so from here we might have heard or if not we'll know that there is an attack called HTTP parameter pollution, <br><br>
HTTP Parameter Pollution: Basically, if we say in easy terms this is not a bug but is used as one because there is no particular standard for servers to handle the parameters. So different server behaves differently when we give multiple parameters of the same name to them.<br><br>
Let's now do it practically for better understanding so now the payload we are going to use is,<br>
Payload: &id=20 <br>
Don't just start throwing queries just now, we are still not done with it.... <br>
Using this parameter,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/cd23fded-0952-4a5d-b4da-f5639b8cd333"><br><br>
On requesting the server with the following URL we get the following response,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/2fdf1a57-9eb7-4530-88f7-55eebfa2a052"><br><br>
Now let's try to add one more ID parameter and see the result, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/69b784ae-221d-4d06-a2ae-86ecb11edf27"><br><br>
So by this, we can at least conclude that this lab is also vulnerable to HTTP Parameter Pollution, and the server will give us the response for the parameter placed far towards the right.<br><br>

Hence we found that this lab has two different ways to access user accounts, The First is our typical IDOR, Second and the new one is by HTTP Parameter Pollution. :)<br>


<h2> LAB 3: Someone changed my Password 🙀!</h2>
Observation: <br>
<br>

<img src=""><br><br>

Solution: <br>
<h2> LAB 4: Change your methods!</h2>
Observation: <br>
<br>

<img src=""><br><br>

Solution: <br>

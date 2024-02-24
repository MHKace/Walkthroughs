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
The first thing we should know about coding a login page with multiple users is parameters should not be displayed and if displayed there should be checks such that these can't be tampered. <br>
> Now as in this URL as marked, we can see the "/profile.php?id=" id parameter, and that too has a numerical value telling us a lot about the backend architecture such as the database at the backend where user profiles are created would have following fields (id, Email, Password, Transaction 1, Transaction 2, Transaction 3), and my user is in the 66th row or is the 66th user. <br>
IDORs are particularly simple we just need to test over these open parameters for the unauthorized information disclosure of other users.<br>
Let's try changing the id value from "id=66" to "id=65", and we can observe<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/0215e6a6-92b2-4124-b586-e0082066db74"><br><br>
And by this, we know our current lab site is vulnerable to IDOR vulnerability.<br>
Before we move on to the next lab let's see if can we get the details of all users.<br>
Let's turn up our Swiss army knife and use it for our testing.<br><br>

<h2> LAB 2: Stop polluting my params!</h2>
Observation: <br>
<br>

<img src=""><br><br>

Solution: <br>
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

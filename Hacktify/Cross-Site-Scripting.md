# Cross-Site Scripting (XSS):

<h2> What is Cross-Site Scripting? </h2>

Cross-site scripting (also known as XSS) is a web security vulnerability that allows an attacker to compromise the interactions that users have with a vulnerable application. Cross-site scripting vulnerabilities normally allow an attacker to masquerade as a victim user, to carry out any actions that the user is able to perform, and to access any of the user's data. If the victim user has privileged access within the application, then the attacker might gain full control over all of the application's functionality and data.

<h2>How does XSS Works?</h2>

Cross-site scripting works by manipulating a vulnerable website's source code/storage system to return malicious JavaScript to users. When the malicious code executes inside a victim's browser, the attacker can fully compromise their interaction with the application by stealing session cookies, user credentials, tokens, secrets, etc.

<h2>Types of XSS: </h2>

    Reflected XSS: The malicious script comes from the current HTTP request when injected into the source code of the application.<br>
    Stored XSS: The malicious script comes from the website's database which eventually gets executed in the user's browser.<br>
    DOM-based XSS: The vulnerability exists in client-side code rather than server-side code. In DOM-based XSS, the malicious user input goes inside the source and comes out of the sink.<br>

<h2>Severity: </h2>

The Reflected XSS has a severity of P3 with a CVSS score of 5.8 which is Medium. This can be used to steal cookies from a victim and also can be used for capturing a victim's credentials.

<h2> Lab 1: Let's Do IT!</h2>
Observations:<br>
As we access the lab we get a page asking us to subscribe to a newsletter as shown,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/0eec7562-50e0-45cb-aff0-ad60d86d5ae3"><br><br>

Solution:<br>
XSS is a great bug as it is found widely but not easily in many cases so it's important that we keep our eyes open and hands moving.<br>
So in this first lab let's dirty our hands and create a methodology to test for XSS which we'll follow but not mention in the solutions in the upcoming labs. Most importantly as we know XSS is when we can insert our custom javascript into a web application.<br>
<br>
Now, for firsts let's check what happens when we enter a random word in the field asking us for input,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/302d4947-13a4-4c23-bcdc-bc47d7f49713"><br><br>
Also, let's check the page source or inspect view for the following to have a better idea of what payload might work wonders for us, (I know you'll say why can't we just insert a js code and say it's vulnerable, so to answer this, "I don't know the answer! So don't bother asking me that.")<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/ecc00ffb-cfa5-4b20-a516-e9a4811e9c9e"><br><br>
By inspecting we can see nothing unusual. <br><br>
Now let's check for HTML injection, huh!! Obviously, some might have already forgotten it so here is the link for the week 1 write-up for <a href="https://github.com/MHKace/Walkthroughs/blob/main/Hacktify/HTML%20Injection.md">HTML injection</a>. <br>
Using payload: <u>MHKace</u> or <u />MHKace, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/7790d6eb-5882-477c-acdd-66e8250c6193"><br><br>
Cool, we can see it's vulnerable to HTML injection, so our next step would be let's check for XSS. <br>
Payload: <script> alert(MHKace) </script>, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/b5e0938f-2a22-4722-89ca-3a238fa858ad)"> <br><br>
What!? our payload didn't work :(, hahahaha! That will happen a lot so chill!<br><br>
Let's just understand one basic thing about js that when you pass 'alert(1)', the above payload will work just fine.... But when we entered 'alert(MHKace)' js treated 'MHKace' as a variable and started a journey to find the variable and which being my name obviously won't be any variable so will not give us an alert box. <br>
New Payload: <script> alert("MHKace") </script>, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/2c0f1798-8cee-4c46-9d21-d283693d764e"><br><br>
Now we can say this lab is vulnerable to XSS.


<h2> Lab 2: Balancing is Important in Life!</h2>
Observations:<br>
We can see a very similar application as we have seen in lab 1, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/a526cee9-d73d-4d60-8851-46a3cb390be8"><br><br>
So let's also look at its source code to know if there are any changes,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/b3c4d763-d372-45d1-9665-2f6a75240e72"><br><br>

Solution:<br>
So, it kind of feels similar to lab 1, let's quickly follow the same steps and dig out the difference, <br>
Testing out for HTML injection gave us the following output,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/c6151b93-0487-4fad-9165-36fa508ee0b5"><br><br>
Looking at the source code we found that our special characters are getting sanitized, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/1a789649-91d4-45f8-8ae1-f090163ad3c7"><br><br>
But wait a minute!! Did you guys notice that, wait let me show you, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/6e50abd5-9771-466d-9c64-cc4434c434e8"><br><br>
We were focusing on the red part so much that we weren't noticing the green part so as we can see red part is getting sanitized for each and all payloads we can use but let's craft a payload to attack the green one,<br>
Payload: "><script>alert("MHKace")</script> <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/c04db307-d20c-4e58-b920-3f55f84ba4d9"><br><br>
Hence, our value parameter is vulnerable to XSS. So we learned an important point it's not that we should always check the content displayed on frontend or over the user interface, but also the parameters or attributes in the page source.<br>

<h2> Lab 3: XSS is everywhere! </h2>
Observations:<br>
On accessing the lab the interface which is thrown at us hasn't changed much...<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/83d286c5-e380-44c9-ba2f-e5fe9a1268b4"><br><br>

Solution:<br>
Like the previous two first let's check for the positions at which our random word gets reflected, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/c6f99b0b-c76c-4e60-b600-c506fbdd6f3b"><br><br>
So we can notice it at two positions one in the body of the page and the other in the URL, of the page, let's attack the URL first as that's something we haven't been doing because it just shows the value of the search box, obviously as we always say if there is just one solution than what was the need for 11 different labs. <br>
<br>
Payload: <script>alert("MHKace")</script><br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/a41d7279-5096-47f3-897c-ec79b95ec241"><br><br>
So by the warning or response thrown in the response we can think of one of the major reasons for our payload not working is not the payload itself but a thing called input validation, Basically in simple words the backed code is checking the input of the search box that it should be in the form of a email, this can be applied as follows,<br><br>
Code Segments:<br>
in PHP:<br>
$is_valid_email = preg_match('/^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/', $email); <br><br>
in javascript:<br>
let isValidEmail = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/.test(email);/<br>
<br>
This is basically a regular expression or regex for input validation.<br>
Now, with this speculation let's craft another payload,<br>
New payload: something@mail.com<script>alert("MHKace")</script>  <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/36b067b4-847c-4fb8-a3c7-6def173489de"><br><br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/208e667c-43ce-4736-9b32-782f64d13b07"><br><br>

So, we can say that the security of this lab is not up to the mark even though it is using the regex and is still vulnerable to XSS attack.

<h2> Lab 4: Alternatives are must!</h2>
Observations:<br>
On accessing the lab the interface which is thrown at us hasn't changed much...<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/83d286c5-e380-44c9-ba2f-e5fe9a1268b4"><br><br>

Solution: <br>
Do we have to even think now? We have the same interface as the previous labs so the same will be our approach.<br>
Let's check for the positions where our value gets reflected. <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/fa933946-8319-4ea5-8e9d-059d96947106"><br><br>
Let's inspect the page source we see that the value is being reflected in two positions, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/997b55c3-824e-4c3e-bdd6-7d18f83a9e9c"><br><br>
Also, we know this lab didn't throw us the response of invalid email as the last one we can conclude that no input validation is going on!! So we can use the following payload, <br>
Payload: "><script> alert("MHKace")</script> <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/52c59653-100d-42c8-8cf1-7c7a2793dba7"><br><br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/408144e2-f96d-4e7f-9d81-846195d295a5"><br><br>
We can notice that the alert is being blocked and now when we focus on the name of the lab we can understand what it means by alternative, let's use the following payloads, <br>
Payloads: "><script>prompt("MHKace")</script> or "><script>print("MHKace")</script><br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/0f5db581-e35e-4989-a6ae-41a98e55bf61"><br><br>

Hence we can say that the following lab is vulnerable to XSS and also we get to learn that there can be many different payloads we can use if we have an understanding of what can be used and when....:)




<h2> Lab 11</h2>
Observations:<br>
![image](https://github.com/MHKace/Walkthroughs/assets/157091170/1851bfc6-8cb6-4507-8d63-dd891e0e3b90)




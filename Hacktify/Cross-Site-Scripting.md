# Cross-Site Scripting (XSS):

<h2> What is Cross-Site Scripting? </h2>

Cross-site scripting (also known as XSS) is a web security vulnerability that allows an attacker to compromise the interactions that users have with a vulnerable application. Cross-site scripting vulnerabilities normally allow an attacker to masquerade as a victim user, to carry out any actions that the user is able to perform, and to access any of the user's data. If the victim user has privileged access within the application, then the attacker might gain full control over all of the application's functionality and data.

<h2>How does XSS Works?</h2>

Cross-site scripting works by manipulating a vulnerable website's source code/storage system to return malicious JavaScript to users. When the malicious code executes inside a victim's browser, the attacker can fully compromise their interaction with the application by stealing session cookies, user credentials, tokens, secrets, etc.

<h2>Types of XSS: </h2>

    Reflected XSS: The malicious script comes from the current HTTP request when injected into the source code of the application.<br>
    Stored XSS: The malicious script comes from the website's database which eventually gets executed in the user's browser.<br>
    DOM-based XSS: The vulnerability exists in client-side code rather than server-side code. In DOM-based XSS, the malicious user input goes inside the source and comes out of the sink.<br>

Severity

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



<h2> Lab 11</h2>
Observations:<br>
![image](https://github.com/MHKace/Walkthroughs/assets/157091170/1851bfc6-8cb6-4507-8d63-dd891e0e3b90)


Lab 1: 

# Clickjacking (UI redressing)

<h2> What is Clickjacking? </h2>

Clickjacking, also known as a “UI redress attack” is an interface-based attack in which a user is tricked into clicking on actionable content on a hidden website by clicking on some other content in a decoy website. In simple words, an attacker uses multiple transparent or opaque layers to trick a user into clicking on a button or link on another page when they intend to click on the top-level page. Thus, the attacker is “hijacking” clicks meant for their page and routing them to another page, most likely owned by another application, domain, or both.
Using a similar technique, keystrokes can also be hijacked. With a carefully crafted combination of stylesheets, iframes, and text boxes, a user can be led to believe they are typing in the password to their email or bank account, but are instead typing into an invisible frame controlled by the attacker.<br>

<h2>How Clickjacking Works?</h2>

Clickjacking uses an iframe to load a vulnerable website on top of an attacker's controlled domain. In the above diagram, you can see there are two web pages let us call them A and B. Website A: A website vulnerable to clickjacking that says "You won a free iPhone!" so that the victim gets lured by "Claiming the Prize!" Website B: It is an attacker-controlled website wherein you have the option to "Pay" This is the exact scenario of how Clickjacking works. Attackers create an attractive website, in our case website A, to lure the victim. Create an iframe and load it in the attacker-controlled domain, website B. In this manner, the attacker manages to fool the victim and make him pay while attracting him for a free prize! So this is how the Clickjacking attack is performed. <br>

<h2>Severity</h2>

Clickjacking-based vulnerabilities are one of simple bugs to find and are classified into two types:<br>
<ul>
    <li>Clickjacking on Non-Sensitive Pages</li>
    <li>Clickjacking on Sensitive Pages</li>
</ul>
Clickjacking on Non-Sensitive Pages is generally considered Informational and categorized as P5 vulnerability whereas Clickjacking on Sensitive Pages is categorized as P4. Clickjacking on sensitive pages can also increase the impact of account takeover and hence can sometimes go up to the P3 category.<br>

<h2> Lab 1: Let's Hijack!</h2>
Observation: <br>
As soon as we land on our lab page we see a user account form where we can fill in user details, and below it is the delete account button which if I have to guess is going to delete this user (WOW... like that's not pretty obvious! :D)<br>
As we explore more we can see a 'Test' button, which looks as follows,
<img href="https://github.com/MHKace/Walkthroughs/assets/157091170/948256c6-2ae5-4fc1-8348-0063aa0d6c9d"><br><br>

Solution: <br>
This lab was no fun, to be honest, I thought we were supposed to write an HTML + CSS code to create an iframe over the delete account button such that when the user clicks on the iframe the account gets deleted.<br>
To kill the fun we have all that done by our stupid 'Test' button. :X <br>
Now as we can see as soon as we click on the 'Delete Account' button a pop-up arises with the following message, <br>
<img href="https://github.com/MHKace/Walkthroughs/assets/157091170/3d38bd41-3f05-4ecf-807a-a9a6f400edae"><br><br>

And now let's see our 'Test' button as soon as we click on the button we are redirected to a screen that looks like, <br>
<img href="https://github.com/MHKace/Walkthroughs/assets/157091170/fa44bef4-7cc1-42d2-b8cc-6a2356deb680"><br><br>
Now, on careful observation 'Spin the Wheel' button overlaps the 'Delete Account' button, and as we click the prior button we get, <br>
<img href="https://github.com/MHKace/Walkthroughs/assets/157091170/60b4a396-e46e-4fb4-ad22-2144efabc882"><br><br>



<h2> Lab 2: Re-Hijack!</h2>

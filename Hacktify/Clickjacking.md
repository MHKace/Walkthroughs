# Clickjacking (UI redressing)

<h2> What is Clickjacking? </h2>

Clickjacking, also known as a “UI redress attack” is an interface-based attack in which a user is tricked into clicking on actionable content on a hidden website by clicking on some other content in a decoy website. In simple words, an attacker uses multiple transparent or opaque layers to trick a user into clicking on a button or link on another page when they intend to click on the top-level page. Thus, the attacker is “hijacking” clicks meant for their page and routing them to another page, most likely owned by another application, domain, or both.
Using a similar technique, keystrokes can also be hijacked. With a carefully crafted combination of stylesheets, iframes, and text boxes, a user can be led to believe they are typing in the password to their email or bank account, but are instead typing into an invisible frame controlled by the attacker.<br>

<h2>How Clickjacking Works?</h2>

Clickjacking uses an iframe to load a vulnerable website on top of an attacker's controlled domain. In the above diagram, you can see there are two web pages let us call them A and B. Website A: A website vulnerable to clickjacking that says "You won a free iPhone!" so that the victim gets lured by "Claiming the Prize!" Website B: It is an attacker-controlled website wherein you have the option to "Pay" This is the exact scenario of how Clickjacking works. Attackers create an attractive website, in our case website A, to lure the victim. Create an iframe and load it in the attacker-controlled domain which is website B. In this manner, the attacker manages to fool the victim and make him pay while attracting him for a free prize! So this is how the Clickjacking attack is performed. <br>

<h2>Severity</h2>

Clickjacking-based vulnerabilities are one of simple bugs to find and are classified into two types:<br>
<ul>
    <li>Clickjacking on Non-Sensitive Pages</li>
    <li>Clickjacking on Sensitive Pages</li>
</ul>
Clickjacking on Non-Sensitive Pages is generally considered Informational and categorized as P5 vulnerability whereas Clickjacking on Sensitive Pages is categorized as P4. Clickjacking on sensitive pages can also increase the impact of account takeover and hence can sometimes go up to the P3 category.<br>

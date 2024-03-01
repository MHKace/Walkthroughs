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
Using payload: &lt;u>MHKace</u> or &lt;u />MHKace, <br>
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
So by the warning or response thrown in the response, we can think of one of the major reasons for our payload not working is not the payload itself but a thing called input validation, Basically in simple words the backed code is checking the input of the search box that it should be in the form of a email, this can be applied as follows,<br><br>
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

Hence we can say that the following lab is vulnerable to XSS and we also get to learn that there can be many different payloads we can use if we have an understanding of what can be used and when....:)

<h2> Lab 5: Developer hates scripts!</h2>
Observations:<br>
On accessing the lab the interface looks similar to other labs we have done so far, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/d019d19d-0aef-4346-8264-1c3db79dbc73"><br><br>
But judging by name we might have to try for something which does contain a '<script>' tag. <br>

Solution:<br>
The best part of a good methodology is its reliability during the process, so let's follow the same method we have followed till now...<br>
I would skip the first step and jump directly to test for HTML injection. <br>
Payload: ">&lt; u> MHKace </u> <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/ab213238-c809-4139-9da0-8e415afe3ef3"><br><br>
Upon checking the source code, we can understand that our main target is the value field as our HTML is getting executed in that as seen above<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/973736d1-0547-4d1e-b5ac-c90a388dc856"><br><br>
Now let's try an XSS payload to test for XSS vulnerability,<br>
Payload: "><script> alert("MHKace")</script> <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/8752a107-deca-4973-bd9b-d5f9abc03d85"><br><br>
When we look at the source code we can see that the '<script>' is being changed to '<scr_ipt>'. <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/eaec162a-88fe-440e-b84d-c109b21945e7"><br><br>
So as we mentioned we need to find a payload that does not have a script tag in it.<br>
Let's try for a payload with '<img>' tag into it,<br>
Payload: ">&lt; img src=X onerror=alert("MHKace")> <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/cede11b2-2970-46f5-9c8e-cea66b8e607d"><br><br>
After solving this lab you might have realized that more than just replicating we need to be creative too, The same payload may never work for all targets so we need the knowledge so that we can slightly tweak and use already available knowledge and hunt for bugs!... Also by this, we could conclude that the following lab has an XSS vulnerability. <br>

<h2> Lab 6: Change the Variation!</h2>
Observations:<br>
HuH!! Again we have the same look and feel, nothing much to say see for yourself, /<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/efb897f6-d77d-4a7b-8dfc-0be269bd838e"><br><br>

Solution:<br>
Looking at the lab we know are first few steps of the process, so let's test for HTML injection,<br>
Payload: ">&lt;u>MHKace</u> <br>

<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/21840e13-c26d-4f22-b371-b89ba4649428"><br><br>
Let's first use our XSS payload and then check our source code if it doesn't work,<br>
Payload: "><script>alert("MHKace")</script> <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/ba8e7af1-ba1c-4ba8-ab3d-9bfa9e9df73a"><br><br>
Let's check the page source for a better understanding of why our payload didn't work,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/ad81707a-c401-4de3-8524-5fb301a317cb"><br><br>
By this we can note that our '<script>' tags are being sanitized, so let's try a different payload than earlier that we used,<br>
Payload: "><img src=x onerror=alert("MHKace")><br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/a00ed7df-6010-4016-b95c-e3b2ab53522a"><br><br>
We might say that this lab is similar to the previous one but before that understand the use case that in the previous one, our script tag was being obfuscated, whereas in this lab our whole script tag is being sanitized. As we are continuously on the path of learning we must know Hacking or Vulnerability Disclosures are all about patience and learning what goes behind the scenes, real-world sites would be much more complicated than the ones we solved easily.<br>

<h2> Lab 7: Encoding is the key?</h2>
Observations:<br>
<i>I am now frustrated, I might just stop writing observation sections they all have the same landing page, and typing the same thing every time feels stupid.</i><br>
Again we have the same look and feel, nothing much to say see for yourself, /<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/efb897f6-d77d-4a7b-8dfc-0be269bd838e"><br><br>

Solution: <br>
Let's follow our methodology to find HTML injection and then leverage it to XSS, <br>
So for this lab let's use the simple HTML payload, <br>
Payload: ">&lt;u>MHKace</u> <br>
<img src="![image](https://github.com/MHKace/Walkthroughs/assets/157091170/94127972-07da-42b8-a2fd-ae0f5b852d03)"><br><br>
This time it's very different to all the above labs, here let's check for the source code to understand what's the show behind the scenes.
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/d5444728-95d6-48f2-950e-960445405278"><br><br>
Now as we can observe this time our payload reflects just in a single position, which is in the body of the page not in the 'input' tag as it does not have a 'value' attribute, also the other thing we can observe is it sanitized our '<', '>', '/' characters, and as the name for this lab says encoding is the key, so let's try to encode our special characters, now the real challenge for us is to find the type of character encoding which our site can manage so the only way to know that is by putting our hands to dirt and I would really appreciate if everyone would read this after finding the encoding by their own as I'll be giving answer to the encoding type further this!!<br><br>

Let's try URL encoding so our payload becomes something like this, <br>
Payload: %3Cu%3EMHKace%3C%2Fu%3E
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/5f66bc69-da95-4ed9-8905-ccc9f18c8f77"><br><br>
As we can observe this worked for us now let us use this same encoding for our XSS payload, <br>
Payload: %3Cimg src=x onerror=alert("MHKace")%3E
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/9ff6d5bb-0a09-40f0-96d7-c14beb38c185"><br><br>
Still not working let's check the page source to know what's the issue, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/614b6ff7-e9ec-4861-aafe-e1a9638153b7"><br><br>
Ohhhh! Now we can see we our '=', '(' and ')' characters are also getting sanitized. Let's encode them too....<br>
Payload: %3Cimg src%3Dx onerror%3Dalert%28"MHKace"%29%3E
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/e81478a3-a2c1-4439-93f4-00bb8ebc1116"><br><br>
Hence, after all those efforts we can now say this site is vulnerable to any type of XSS payload if the attacker could just send encoded special characters.<br>

<h2> Lab 8: XSS with File Upload (file name)</h2>
Observations:<br>
After a long, while we could see something different, on accessing the lab we can see a page that allows us to upload a file as shown,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/845d5554-d6d5-4172-8f3d-e55e7c0aa22a"><br><br>
We see the following interface after successfully uploading the file, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/96295b81-768e-437a-87d0-73c9417ee323"><br><br>


Solution:<br>
As the name of the lab suggests we will narrow down our testing to the name of the file if we remember we did the same kind of lab in the HTML injection section. <br>
So, we'll follow the same steps as we did back then, to check whether the file name is vulnerable to HTML injection or not, <br><br>
Let's power up our burp to intercept the request made to upload the file, and capture the request, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/14c16d8e-3f03-410d-a989-804735af1a5d"><br><br>
Now, we'll use the same payload as before, <br>
Payload: &lt;u> (before file name)<br>
We get the following result, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/f94f564c-ec37-4313-b542-dee727485de1"><br><br>
Now as our reflected filename parameter is susceptible to HTML injection attack let's try our payload for XSS,<br>
Payload: &lt;img src=x onmouseover=(1)><br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/2a8a6e8a-4c63-4410-b2a8-fba87618363a"><br><br>
Now some reasoning behind using this payload, our parameter is not rendering or processing the close tags and tags are only working before the file name, so we needed a payload that just has an opening tag and this requirement is fulfilled by our 'img' tag.<br>
On forwarding the request we get, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/7c36c94f-81e6-4891-8776-d9e583dc7bc9"><br<br>
Hence we can conclude that the filename parameter is vulnerable to XSS attack.<br>



<h2> Lab 9: XSS with File Upload (File Content)</h2>
Observations:<br>
This lab seems similar to the last lab but we can know by the name of the lab and the look of it our file content will get printed/executed. The lab looks something like,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/6b95a271-40c6-4c26-aa49-1560c370829b"><br><br>
On uploading a file we can see the following response,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/2e8bca3a-b6bc-433e-8dc9-76972f705ea2"><br><br>

Solution:<br>
I sometimes feel like it would be better if I just ask someone else to type all this for me but it'll cause the loss of originality that fun and curious element that you guys get in my write-ups, actually solving labs is pretty much easy but for me, the goal is to learn the technology, methodologies, and complexities faced. Also, I feel good when my keyboard is sounding like crazy when I am typing really fast!! :)<br><br>
Let's craft a payload file to check HTML injection same as in labs we did last week!!<br>
Payload: <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/6afe10a8-3dcc-4230-b621-bde5405e2cda"><br><br>
Uploading this file gave us the following result, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/baf8c601-f8aa-4799-a1f8-b12fbd6af593"><br><br>
Now let's test for XSS so initially let's try a basic payload added to the file, <br>
Payload:<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/af4e4d4a-d959-498b-a119-bccf8a6988b6"><br><br>
On uploading this payload file it gave us the following response,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/6df9f43f-fe31-4c01-af90-ec255f66823a"><br><br>
This concludes that the file content can also be an attack vector to find the XSS.<br>

<h2> Lab 10: Stored Everywhere!</h2>
Observations:<br>
Now this lab gives us a login page, which looks something like this,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/734c1fb5-5e8d-4b98-aed3-0919c8c6d36d"><br><br>
Let's register our user by visiting the register page, which will look something as<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/b8ba6c7f-0029-43b6-be94-96f084b88cb3"><br><br>

Solution:<br>
Now after following the methodology for about 9 labs, we are more than familiar with the process, so for this lab let's go berserk and test it directly for XSS, so now we'll just be using one simple payload on every position we can see,<br>
Payload: ">&lt;img src=x onmouseover=alert("MHKace")> <br>
So, we did something like this,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/9c84c3df-740f-40a1-90bd-2e6888492799"><br><br>
Basically, we have filled following details, <br>
First Name: ">&lt;img src=x onmouseover=alert("MHKace")><br>
Last Name: ">&lt;img src=x onmouseover=alert("MHKace")><br>
Email: something@mail.com">&lt;img src=x onmouseover=alert("MHKace")><br>
Password: ">&lt;img src=x onmouseover=alert("MHKace")><br>
<br>
And now when we log in using the same email and password, we get to see the following response,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/72296e6d-ebb0-4301-9050-4eaca3239d3b"><br><br>
As we used 'onmouseover' function we got the following result when we hovered our mouse pointer over the image icons, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/7fd10990-949c-4ef2-8782-f5a5cf6a8cc4"><br><br>
We can say our lab had stored XSS vulnerability in it.<br>
<br>
Now the confusion arises,  what is the difference between self, reflected, and stored XSS?? <br>
So an XSS payload that can be seen in your source code or is reflected and successfully executes is called reflected XSS, also this crafted source code or URL can be sent to other users, which leads to threats such as cookie stealing, uploading malicious code, etc. <br>
On the other hand, a self-XSS is a kind of reflected XSS that can be seen in one's own browser but when the crafted source code or URL is sent to someone else it does not execute, so the impact of self-XSS is very low and most times we are not paid bounties for those.<br>\
A stored XSS is on the other hand a high-paying bug as the XSS payload in it is not just reflected in the source code but is stored in the backend server so it gets executed as many times a user visits it.<br>


<h2> Lab 11: DOM's are love!</h2>
Observations:<br>
There isn't much for us to look at in this lab,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/5928dcd6-ff98-4cd2-8847-778dc83bc0de"><br><br>
Let's also look at the source code for a better understanding of the web page in front of us, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/77cf1976-3bd9-43b2-93ba-1e88e54656b4"><br><br>
We can see it has another file named 'dom.js' On visiting the js file we can see the following piece of code, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/7deb6dea-358c-411b-8fb0-a5ede43d298e"><br><br>


Solution:<br>
Finally, this is our last lab for XSS and I would really apologize to everyone for not being able to send out all the write-ups early, So with that let's hack into this lab.....:)<br>
Looking at initial page we knew that there is nothing we can find there which is injectable, but the lab talks about 'DOM' so we have some idea that there should be some value which user enters will be reflected or shown on the frontend, <br>
Unable to find anything on the frontend or landing page, we went digging into source code and there we found a file named 'dom.js' as observed before and as we can look into the file, we can locate quite a few parameters to play with, listed as<br>
<ul>
    <li>?name=</li>
    <li>?redir=</li>
    <li>?coin=</li>  
</ul>
<br><br>
Knowing we don't slack off we'll at least check for the bug in two of those....<br>
<br>
Let's first try using '?name=' parameter and giving a random name, <br>
Payload: URL?name=MHKace <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/b76f9bd2-3232-4f26-bdc0-8313ca2f20b4"><br><br>
Ohkay! now we need to craft a payload to exploit this, so now the biggest payload crafting tip would be to look at the code and craft, what would be the best thing and whether will it work or not, or how the inserted payload will be treated by the backend.<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/9c225a83-d67c-48cf-a6dc-f49d5e2a2731"><br><br>
Looking at the following piece of code we need to craft a payload, <br>
Payload: "&lt;img src=x onerror=alert("MHKace")>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/d2751970-2494-4859-87c9-a5ad8b40bf50"><br><br>
A bit too easy right?? Crafting a working payload in real life is a big hassle, so it's always advised to have a bit of knowledge about the technology you are testing.<br><br>

Now testing our second parameter '?redir=', gives,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/3a127903-a81d-447d-9914-bce4a421370c"><br><br>

This could be a rare finding as Reading this piece of code I didn't want to test this parameter for XSS, by going through the name of the parameter I wanted to see whether this parameter can redirect me or the victim to any random webpage,<br>
Payload: URL?redir=http://www.vulnweb.com <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/4471ab5f-b997-4e07-8941-270f6b38e0a0"><br><br>
On requesting the following URL in response I received,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/c7cc202c-a510-48ab-9ea5-4f10b729ef64"><br><br>
Now, Let's try using '?coin=' parameter and giving a random name, <br>
Payload: URL?coin=MHKace <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/be459410-bc66-461d-8ee6-43f053972570"><br><br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/98bf83f7-9dac-4a5a-b474-55d34653ea92"><br><br>
Looking at the following piece of code we need to craft a payload, <br>
Payload: "&lt;img src=x onerror=alert("MHKace")>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/dbeab717-3960-4f1e-bca6-88b2ad41df41"><br><br>
We can conclude that our lab is vulnerable to XSS for '?name=' and '?coin=' parameters and it is also vulnerable to open redirect on its '?redir=' parameter as it enables the attacker to craft and redirect to a random web page. <br><br>


Happy Hacking!!<br>
MHKace  :)

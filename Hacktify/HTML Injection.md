# HTML Injection

<h2>What Is HTML?</h2>
HTML stands for Hypertext Markup Language. It is a standard markup language for web pages. A collection of web pages makes a website. HTML elements are represented by <> tags. Where each tag has a different working. <br>
A resource to learn HTML: <a href="https://www.w3schools.com/html/"> click here </a> <br><br>

<h2>What Is HTML Injection Attack?</h2>
HTML Injection is a vulnerability that occurs in web applications that allow users to insert HTML code via a specific parameter or an entry point. HTML Injection is an attack that is similar to Cross-site Scripting (XSS). While in the XSS vulnerability the attacker can inject and execute Javascript code, the HTML injection attack only allows the injection of certain HTML tags. When an application does not properly handle user-supplied data, an attacker can supply valid HTML code, typically via a parameter value, and inject their content into the page. It is generally exploited using social engineering to trick valid users of the application into opening malicious websites or to insert the credentials in a fake login form that will redirect the users to a page that captures cookies or credentials. <br><br>

<h2>Severity</h2>
The severity of HTML Injection can be categorized as a P4 bug with a CVSS score of 0.1-3.9 which is Low. In case of an account takeover, it can be categorized as P3.<br>


<h2> Logging in {felt this was the most asked question in a while... :D}</h2> <br>
As instructed to access labs we have to follow the following path, <br>
Search => Hacktify.in > Resources > labs > login <br>

To log in as instructed we need to enter our registered email ID in both the fields email-id and password field, <br>
For example: 
<ul> <li>email-id: xyz@mail.com</li>
<li>password: xyz@mail.com</li> 
</ul><br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/9d5909be-00f8-4313-8e0b-cca2d01bfaae"  >
<br>

<h2> LAB 1: HTML's are easy!</h2> <br>
Observation: <br>
On accessing the lab we can observe the following UI. <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/7347473e-3847-48b0-97c4-51f0afe7c33d"  >
<br>
<br>
Solution: <br>
The first thing to test for an HTML injection is we need to check whether or not our input field value is being reflected somewhere on the page/source code or is being stored(we'll talk about this in an upcoming lab). <br><br>
So, let's enter my name into our search bar/box. <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/0e85333a-f51c-4e8a-8cbf-f5dc8fb9e456"  >
<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/456af1bc-e142-416f-a71c-f3a8d50f1674"  > <br>
We can see the value is reflected on the UI and also over the source code. <br><br>
The next step we can do to test for HTML injection is to try a payload "&lt; h1> MHKace &lt; /h1>" in the search bar to check whether the user input HTML is being executed or not. <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/a847960b-e2b0-4bec-9e13-45ff3b75492c"  ><br>
On using the payload we can observe the following response,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/e2a57f48-b9e2-4c98-a683-1e0b8017c5f8"  >
<br><br>
This confirms that the search parameter is vulnerable to HTML injection.<br><br>



<h2> LAB 2: Let me Store them!</h2> <br>
Observation: <br>
On accessing the lab we land on a login page where we are required to enter our email ID and password to get access to the user account also provides a 'Register' button which takes us to a page asking us for basic details to create a user account. The pages look like these,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/8b76e302-ca5c-4a36-ae2e-b4cbc197fccd">
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/05d00048-eeae-45cc-90af-299c7c197613"><br><br>
Solution: <br>

Firstly let's check by entering a random email ID and password on the landing page to check whether any of the values(mostly email ID would be reflected such as "xyz@mail.com is not a valid email ID"...or something like that)<br> <br>
NO LUCK!! :(  [p.s. shortcuts rarely work.]<br>
Let's go to the register page and create a user to log in,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/817455e7-6703-4816-86b0-d8fbd72a027c"><br><br>
Now let's log in using the same email ID and password we used to create our user i.e. email ID - xyz@mail.com and Password - 123 <br>
Upon logging in, we are directed to a page resembling the registration form. However, in this instance, the fields are pre-filled with the information we provided when initially creating our dummy user.<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/ff882d30-160e-430a-8a93-5cb84f82bece"><br><br>

Now that we have a clear idea of what should we be doing, let's log off this user and create a new user using the following values for each field,<br>
First Name: " &quot;>&lt; h1> MHK &lt; /h1> "<br>
Last Name: "&quot;>&lt; h1> ace &lt; /h1> "<br>
Email-id: "asdf@email.com" <br>
Password: "123" <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/87909972-cc5f-4a3d-90b1-deb544fd1248"><br><br>
As we log in using this new user (i.e. abc@mail.com) we observe,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/3d825f96-ddd9-400f-982e-936fcd1b47cb"><br><br>

The fields with our crafted payloads show the first name and last name of the user in the heading format which concludes that our fields were vulnerable to stored HTML injection.<br> <br>

<h4> Reflected HTML injection vs Stored HTML injection: </h4>
The HTML injection we performed in lab 1 is called reflected HTML injection as the payload we entered in the search box persists only in our current browser session whereas a stored HTML injection would persist even if you log out of your account. (The best way to test it is to make your account in a browser take Firefox and then close the labs there log in to labs in Chrome go to lab 2 and enter the same email ID pass "asdf@email.com" and "123" You can observe that payload persists as stored HTML injection let's attacker store the payload at server side and hence is more impactful than reflected.)<br><br>





<h2> LAB 3: File Names are also vulnerable!</h2> <br>
Observation: <br>
On accessing this lab we can notice a file upload feature with a browse file button and an upload button, nothing fancy!! :)<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/9be23fb7-763b-4c38-95b6-07d0f4d35ae5">
<br><br>
Solution: <br>
The best way to know how something works or find a flaw is to use the feature and notice the changes, following this thought on uploading a file we can notice this in our lab,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/6dbb0724-a8b8-4bb3-a5bd-2f7debde5b0a"><br><br>
Now I don't know how many of you are familiar with Burp Suite so we'll keep the complexity of using it to as minimum as possible.<br><br>
To be clear Burp Suite is a Swiss army knife for hackers, and one of its main features is that it acts as a proxy between the source and the destination, and the most common usage is intercepting the requests from the source machine/browser/tab(s).<br>
Let's intercept the request when we hit the upload button and analyze it in Burp Suite, the request looks something like this,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/7ca08a00-82c0-4e44-9837-7fa84a59bc6f"><br><br>
We can see the filename in the request now the next thing is to add a payload so one way could be to add a "&lt; h1>" tag before the filename such as,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/71a235df-753c-463b-91e3-b264ae4b2a0b"><br><br>
Then forward this crafted request and we get the following response,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/1ac3b477-3c66-4f65-8e12-699204118e6c"><br><br>
This observation suggests that the "filename" parameter, utilized to display the name of the uploaded file, lacks proper sanitization. Consequently, this enables the insertion of client-side scripts into the code.<br><br>

Note: It's always a game of trial and error, in these walkthroughs we are just using a single tag to test the vulnerability but of course, in real-world scenarios, these general tags are mostly blacklisted so we need to try with multiple HTML tags. Also if we notice here only an opening tag is being utilized and the closing tag is displayed with the file name if you use the following payload "&lt; h1> file_name &lt; /h1>". So, that's what we say "Hacking or penetration testing is the game of trial and error."<br><br>



<h2> LAB 4: File Content and HTML Injection a perfect pair!</h2> <br>

Observation: <br>
As soon as we land on the webpage for this lab the frontend looks similar to the previous lab, but the person who styled the div might be still learning the CSS as he left it too large :D.
<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/4cfa7cf9-7395-4f93-934f-d1c6323bccbe"  >
<br><br>
Solution: <br>
The best human trait is we learn, we gain experience and we already have the knowledge that our ancestors worked thousands of years and we start from the point they stopped. 
The best example would be "We don't invent the wheel, that's already done! we study about it and utilize it to make cars."<br>

The reason to state this was, to try to do what we have previously done, so we won't discuss the testing we already did in the previous lab and directly jump to what else can we do with this lab.<bR><br>
Reading the name of the lab gave a big hint! So without a delay, we can jump to our code editors or notepad and start typing a basic HTML code and save it into a file, let's say hello.html, and upload it. <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/4f01a213-31a8-4594-946b-8f0318c8097b"><br><br>
On uploading this file we might see the following output, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/e44fae6f-84e6-4962-8a5b-0a75b90a385a"><br><br>

This concludes that our backend does not check the type of file being uploaded and it also lets us parse and execute the file as it is... in most similar cases in the real world this could lead to shell upload resulting attacker gaining access to the server. <br><br>


<h2> LAB 5: Injecting HTML using URL</h2> <br>
We are reaching the end of our lab this will be our second last and by far the toughest lab for me, so stay put, and let's hack it. <br>
<br>
Observations: <br>
On accessing the lab we can observe that there is no injectable parameter like the labs we have done until this point but we can observe that the URL is displayed on the landing page of the lab as follows, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/c5c921a1-67d5-46d4-90e7-741d048f5586"  >
<br>
<br>
Solution: <br>
After wrecking my brain and almost trying everything, I had an idea...<br><br>
The question we need to answer is, "Is the URL printed on the frontend hardcoded, or is getting fetched?"<br>

<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/322e5f6f-7979-41a5-8693-2cfeaccd8ab1"  ><br><br>
To check this We need to check the source code for the lab. <br>

<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/0cec7ef7-c05a-4f5f-bf91-6938567715e4"  ><br><br>
We all will get something like this, but this does not answer our question, so to get the answer let's play with the the URL for our lab. <br><br>
<i> Note: If the URL marked in the above image is hardcoded it won't get altered but if it's the copy or is getting fetched from the server same as the URL of our lab it will change. (I hope that made some sense:X) <br> </i> <br>
Let's add a parameter to our URL, Let's say "?id="<br>

<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/53f979e4-d6d1-4e96-883f-18de8f0e9080"  ><br><br>
Now on hitting enter to this change, we get, <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/cb3936c3-c3a6-477b-b459-93fde4a762f9"  ><br><br>
That gives us the most important information that our UI is getting fetched from the server-side script to the URL we search for, <br><br>
Now let's use the following payload and observe what happens, "?id=&lt h1>MHKace&lt /h1>" <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/f2ff51eb-6f76-4430-82bd-9d5d03787060"  ><br><br>
On noticing the outcome we can conclude that the queries in the URL are not being filtered/sanitized which is the cause for our URL to be susceptible to HTML injection attacks. <br><br>



<h2> LAB 6: Encode IT!</h2> <br>
Observation: <br>
Finally, the end of the section, on accesing the lab we can observe we are back to the view of lab 1 easy peasy!!
<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/c8ca5715-5b6f-4514-b1c3-4076bfae2d4a"><br><br>
Solution: <br>
As soon as we see a similar situation we try whatever we have already did to the similar cases so let's use the payload form lab 1 i.e., "&lt; h1> MHKace &lt; /h1>" <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/593d19eb-7568-4ba8-8b82-472116327d2e"><br><br>
and let's observe the response,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/f9198475-fa34-4ab9-a974-29a2a1ca04bb"><br><br>
:X Obviously, we don't get anything easily, but looking at the response we can tell there is a filtering going on the backend for the values of search parameter of this lab and as per my understanding of development, here blacklisting is implemented,<br><br>
<strong> Blacklisting:</strong> It is just a method to restrict a particular or a set of values in simple words. <br><br>
So, a code at the backend could be something like following:<br><br>
$output = str_replace(array('<', '>'), ';', $inputString); <br>
This php code will replace angular('<' '>') brackets with semicolon(';') <br><br>
let outputString = inputString.replace(/[<>]/g, ';');<br>
A javascript code to replace angular('<' '>') brackets with semicolon(';') <br><br>

So we just need to not use angular bracket, and the name for our lab is also encode it! so why not encode our angular brackets using URL encoding,<br>
"<" => "%3c"  <br>
">" => "%3e"  <br>
<br>
So our new payload can be, "%3ch1%3e MHKace %3c/h1%3e" <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/e6e2fe69-87f8-4bec-b779-3ffe0f5f189f"><br><br>
Let's see the response to our new payload,<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/7f7bfb72-024f-44e6-a093-5e9e2cd839bb"><br><br>
And we did it!! By this we can say we ended all our labs for HTML injection, but the world is too wide to cover in just 6 labs, a small task try reading about different encoding schemes/techniques and try to use them and see what all works.<br>
<i>Note: Whitelisting is always better than Blacklisting it gives us more granular control. </i><br><br>
Thanks for bearing with this write-up/walkthrough! :) <br>
Happy Hacking.......

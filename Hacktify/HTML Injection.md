# HTML Injection

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
The next step we can do to test for HTML injection is to try a payload "&lt h1> MHKace &lt /h1>" in the search bar to check whether the user input HTML is being executed or not. <br>
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

Reflected HTML injection vs Stored HTML injection => The HTML injection we performed in lab 1 is called reflected HTML injection as the payload we entered in the search box persists only in our current browser session whereas a stored HTML injection would persist even if you log out of your account. (The best way to test it is to make your account in a browser take Firefox and then close the labs there log in to labs in Chrome go to lab 2 and enter the same email ID pass "asdf@email.com" and "123" You can observe that payload persists as stored HTML injection let's attacker store the payload at server side and hence is more impactful than reflected.)<br><br>





<h2> LAB 3: File Names are also vulnerable!</h2> <br>
Observation: <br>
On accessing this lab we can notice a file upload feature with a browse file button and an upload button, nothing fancy!! :)<br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/9be23fb7-763b-4c38-95b6-07d0f4d35ae5">
<br><br>
Solution: <br>





<h2> LAB 4: File Content and HTML Injection a perfect pair!</h2> <br>
Observation: <br>
<br>
<img src=""  >
<img src=""  ><br><br>
Solution: <br>




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
<br>
<img src=""  >
<img src=""  ><br><br>
Solution: <br>

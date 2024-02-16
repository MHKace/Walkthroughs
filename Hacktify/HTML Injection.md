# HTML Injection

<h2> Logging in {felt this was the most asked question in a while... :D}</h2> <br>
As instructed to access labs we have to follow the following path, <br>
Search => Hacktify.in > Resources > labs > login <br>

To log in as instructed we need to enter our registered email ID in both the fields email-id and password field, <br>
For example: 
<ul> <li>email-id: xyz@mail.com</li>
<li>password: xyz@mail.com</li> 
</ul><br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/9d5909be-00f8-4313-8e0b-cca2d01bfaae" alt="Screenshot 2024-02-16 210506">
<br>

<h2> LAB 1: HTML's are easy!</h2> <br>
Observation: <br>
On accessing the lab we can observe the following UI. <br>
<img src="https://github.com/MHKace/Walkthroughs/assets/157091170/7347473e-3847-48b0-97c4-51f0afe7c33d" alt="Screenshot 2024-02-16 210506">
<br>
<br>
Solution: <br>
The first thing to test for an HTML injection is we need to check whether or not our input field value is being reflected somewhere on the page/source code or is being stored(we'll talk about this in an upcoming lab). <br><br>
So, let's enter my name into our search bar/box. <br><br>
![text](https://github.com/MHKace/Walkthroughs/assets/157091170/0e85333a-f51c-4e8a-8cbf-f5dc8fb9e456)
<br><br>
![image](https://github.com/MHKace/Walkthroughs/assets/157091170/456af1bc-e142-416f-a71c-f3a8d50f1674)<br><br>
We can see the value is reflected on the UI and also over the source code. <br><br>
The next step we can do to test for HTML injection is to try a payload "&lt h1> MHKace &lt /h1>" in the search bar to check whether the user input HTML is being executed or not. <br>
![image](https://github.com/MHKace/Walkthroughs/assets/157091170/a847960b-e2b0-4bec-9e13-45ff3b75492c)<br><br>
On using the payload we can observe the following response,<br>
![image](https://github.com/MHKace/Walkthroughs/assets/157091170/e2a57f48-b9e2-4c98-a683-1e0b8017c5f8)
<br><br>
This confirms that the search parameter is vulnerable to HTML injection.<br><br>

<h2> LAB 5: Injecting HTML using URL</h2> <br>
We are reaching the end of our lab this will be our second last and by far the toughest lab for me, so stay put, and let's hack it. <br>
<br>
Observations: <br>
On accessing the lab we can observe that there is no injectable parameter like the labs we have done until this point but we can observe that the URL is displayed on the landing page of the lab as follows, <br><br>
![image](https://github.com/MHKace/Walkthroughs/assets/157091170/c5c921a1-67d5-46d4-90e7-741d048f5586)
<br>
<br>
Solution: <br>
After wrecking my brain and almost trying everything, I had an idea...<br><br>
The question we need to answer is, "Is the URL printed on the frontend hardcoded, or is getting fetched?"<br><br>
![Screenshot 2024-02-16 214017](https://github.com/MHKace/Walkthroughs/assets/157091170/322e5f6f-7979-41a5-8693-2cfeaccd8ab1) <br><br>
To check this We need to check the source code for the lab. <br><br>
![image](https://github.com/MHKace/Walkthroughs/assets/157091170/0cec7ef7-c05a-4f5f-bf91-6938567715e4) <br><br>
We all will get something like this, but this does not answer our question, so to get the answer let's play with the the URL for our lab. <br><br>
<i> Note: If the URL marked in the above image is hardcoded it won't get altered but if it's the copy or is getting fetched from the server same as the URL of our lab it will change. (I hope that made some sense:X) <br> </i> <br>
Let's add a parameter to our URL, Let's say "?id="<br><br>
![image](https://github.com/MHKace/Walkthroughs/assets/157091170/53f979e4-d6d1-4e96-883f-18de8f0e9080)<br><br>
Now on hitting enter to this change, we get, <br><br>
![image](https://github.com/MHKace/Walkthroughs/assets/157091170/cb3936c3-c3a6-477b-b459-93fde4a762f9) <br><br>
That gives us the most important information that our UI is getting fetched from the server-side script to the URL we search for, <br><br>
Now let's use the following payload and observe what happens, "?id=&lt h1>MHKace&lt /h1>" <br><br>
![image](https://github.com/MHKace/Walkthroughs/assets/157091170/f2ff51eb-6f76-4430-82bd-9d5d03787060) <br><br>
On noticing the outcome we can conclude that the queries in the URL are not being filtered/sanitized which is the cause for our URL to be susceptible to HTML injection attacks. <br><br>

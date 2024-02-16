# HTML Injection

<h2> Logging in {felt this was the most asked question in a while... :D}</h2> <br>
As instructed to access labs we have to follow the following path, <br>
Search => Hacktify.in > Resources > labs > login <br>

To Login as instructed we need to enter our registered email id in both the fields email-id and password field, <br>
For example: 
<ul> <li>email-id: xyz@mail.com</li>
<li>password: xyz@mail.com</li> 
</ul><br>
![Screenshot 2024-02-16 210506](https://github.com/MHKace/Walkthroughs/assets/157091170/f5911f04-1d76-4f0d-be86-bc59f545bc21)
<br>

<h2> LAB 1: HTML's are easy!</h2> <br>
Observation: <br>
On accessing the lab we can observe the following UI.
![image](https://github.com/MHKace/Walkthroughs/assets/157091170/7347473e-3847-48b0-97c4-51f0afe7c33d)

The first thing to test for a HTML injection is we need to check whether or not our input field value is being reflected somewhere on page/source-code or is it being stored(we'll talk about this on an upcoming lab). <br>
So, let's enter my name into the search bar/box we have. 
![image](https://github.com/MHKace/Walkthroughs/assets/157091170/0e85333a-f51c-4e8a-8cbf-f5dc8fb9e456)
![image](https://github.com/MHKace/Walkthroughs/assets/157091170/456af1bc-e142-416f-a71c-f3a8d50f1674)

We can see the value is reflected on the UI and also over the source code. <br>

> The next step we can do to test for HTML injection is try a payload "<h1> MHKace </h1>" in the search bar to check whether the user input HTML is being executed or not.
![image](https://github.com/MHKace/Walkthroughs/assets/157091170/a847960b-e2b0-4bec-9e13-45ff3b75492c)
On using the payload we can observe the following response,
![image](https://github.com/MHKace/Walkthroughs/assets/157091170/e2a57f48-b9e2-4c98-a683-1e0b8017c5f8)

And this confirms that the search parameter is vulnerable to HTML injection.

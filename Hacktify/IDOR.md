# IDOR (Insecure Direct Object Reference)

<h@> What is Insecure Direct Object References Attack?</h2> <br>

An insecure direct object reference (IDOR) is an access control vulnerability where invalidated user input can be used for unauthorized access to resources or operations. It occurs when an attacker gains direct access by using user-supplied input to an object without authorization. Attackers can bypass the authorization mechanism to access resources in the system directly by exploiting this vulnerability. Every resource instance can be called an object and often, represented with an ID. And if these IDs are easy enough to guess or an attacker can use an object to bypass the access check somehow, we can talk about an IDOR at this point. Referring to the above image, an attacker by ethical means can only get the document numbered 101 which is legally his. But what if the web application does not validate the number and an attacker puts the number of its victim? This can cause the attacker to get hold of the sensitive document to which he should not have access. <br>

<h2> Severity: </h2><br>

The severity of IDOR varies from P3 to P2 depending on what data is being exposed.<br>

<h2> LAB 1: Give me my amount!!</h2>
<h2> LAB 2: Stop polluting my params!</h2>

<h2> LAB 3: Someone changed my Password 🙀!</h2>

<h2> LAB 4: Change your methods!</h2>

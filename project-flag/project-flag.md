---
title: Project Flag Report
author:
  - christopher_freytes@brown.edu
  - 'Brown ID: B01792886'
date: '2023-03-05'
subject: Markdown
keywords:
  - Markdown
  - Example
subtitle: Project Flag Report
lang: en
titlepage: true
titlepage-color: 1E90FF
titlepage-text-color: FFFAFA
titlepage-rule-color: FFFAFA
titlepage-rule-height: 2
book: true
classoption: oneside
code-block-font-size: \scriptsize
mainfont: System font, sans-serif
---

# Project Flag Report

## Introduction

Web Security is a pivitol topic, and a deep understanding of the possible web expliots, allows for a better graspse on how to defend against them. The purpose of this project is to put into practice the topics discussed in CS1660.

## Objective

This assignment centers around five distinct vulnerabilities found within the FLAG Portal. All of the exploits center around, obtaining unauthorized access. Lastly, the following wiki was referenced for clarity: <https://cs.brown.edu/courses/csci1660/wiki/>

# Vulnerability Category: SQL Injection Attack

- Go to Login Page

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image1.png){width=50%}
  
- Open Firefox Developer Tools

- Change the onsubmit parameters to: ```onsubmit="return true"```

```htm
<form id=\"comment-form\" action=\"profile.php?id=26\" method=\"post\"
style=\"margin-top:20px\" onsubmit=\"return
validateCommentForm();\"\>\<textarea rows=\"4\" name=\"comment\"
placeholder=\"Write a comment here\...\"\>\</textarea\>\
<input type=\"submit\" value=\"COMMENT\" style=\"margin-left: auto;
margin-right: auto;\"\> \</form\>
```

- Enter: ``` admin" OR 1=1-- ``` without a password

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image3.png){width=50%}

## Impact

The impact of a SQL injection attack can be significant, ranging from financial losses to reputational damage, legal consequences, and even physical harm. A SQL injection attack can also compromise the integrity and availability of the database. The attacker can delete, modify, or extract data from the database, causing disruption to the organization's operations and services. 

## Mitigation

Here are some mitigation strategies to prevent SQL injection attacks:

Parameterized Queries: Use parameterized queries or prepared statements, which can help prevent SQL injection by separating SQL logic from user input. Prepared statements provide a way to send the SQL query and parameters to the database separately, eliminating the risk of SQL injection.

Input validation and sanitization: Validate and sanitize all user input. Validate input to ensure it matches the expected data type, format, and length. Sanitize input to remove any potentially malicious characters or code.

Principle of Least Privilege: Apply the principle of least privilege, which means limiting the privileges of users and applications to the minimum necessary to perform their tasks. This can help reduce the damage that an attacker can do if they successfully inject malicious SQL code.

Use Web Application Firewalls: Implement a web application firewall (WAF), which can help detect and block SQL injection attacks. A WAF sits between the web application and the internet, monitoring traffic for signs of attack and blocking any malicious requests.

Keep Software Up-to-Date: Keep your web application and database software up-to-date with the latest patches and security updates. This can help prevent SQL injection attacks by addressing known vulnerabilities.

Logging and Monitoring: Log and monitor all database activity and user input to identify any potential SQL injection attacks. This can help detect attacks in real-time and allow for quick mitigation.


# Vulnerability Category: XSS Attack

- Login to the Website using: ```qmei```

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image1.png){width=50%}

- Go to the profile page

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image4.png){width=50%}

- Change the onsubmit parameters to ```onsubmit=\"return true\"```

```htm
<form id=\"comment-form\" action=\"profile.php?id=26\" method=\"post\"
style=\"margin-top:20px\" onsubmit=\"return
validateCommentForm();\"\>\<textarea rows=\"4\" name=\"comment\"
placeholder=\"Write a comment here\...\"\>\</textarea\>\
<input type=\"submit\" value=\"COMMENT\" style=\"margin-left: auto; margin-right: auto;\"\>\</form\>

```

- Add the following to the comment box: ```<scrscriptipt> alert(Something)</script>```

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image5.png){width=90%}

## Impact

An XSS (Cross-Site Scripting) attack is a type of web-based attack that involves injecting malicious code into a website, usually through a vulnerable input field such as a search box or a comment section. 

The impact of an XSS attack can be severe, depending on the nature and scope of the attack. Here are some possible consequences:

Data theft: An attacker can use XSS to steal sensitive information, such as credit card details, social security numbers, or login credentials. This information can be used for identity theft or fraud.

Website defacement: An attacker can inject code that alters the appearance or content of a website, leading to reputational damage or loss of business.

Malware distribution: An attacker can use XSS to distribute malware, such as ransomware or spyware, to users who visit the compromised website.

Account hijacking: An attacker can use XSS to hijack a user's account, giving them access to the user's personal information and the ability to carry out actions on their behalf.

## Mitigation

Input validation: Developers should ensure that all input data is properly validated to prevent malicious code from being injected into the web application.

Output encoding: Encoding user input data before displaying it on the web page can prevent the execution of malicious scripts.

Secure cookie handling: Ensuring that cookies are properly scoped and marked with secure and HTTPOnly flags can prevent attackers from stealing sensitive user data.

Content Security Policy (CSP): Implementing a CSP header can restrict the sources from which a page can load external resources, such as scripts, stylesheets, or images. This can prevent attackers from injecting malicious scripts into the page.

Use of HTTPS: Implementing HTTPS can ensure that the communication between the client and the server is secure, preventing attackers from intercepting sensitive data, including cookies.

# Vulnerability Category: Insecure Direct Object Reference

- Login to the Website using ```qmei```

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image1.png){width=50%}

- Go to the grades page

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image6.png){width=50%}

- View any submission

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image7.png){width=50%}

- Observe how the url directory is ```/handins/```

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image8.png){width=90%}

- Browse to: ```http://localhost:8888/handins/```

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image9.png){width=50%}

- Another example: ```http://localhost:8888/handouts/```

- All ```/handins/``` can be see no matter if you are logged-in or not

## Impact

Insecure Direct Object Reference is a common vulnerability that arises when an application allows an attacker to access and manipulate resources directly by referencing a specific identifier or key. The attacker can exploit this vulnerability by changing the value of the identifier and accessing resources that should not be accessible to them.

## Mitigation

To mitigate IDOR attacks, the following measures can be taken:

Access Control: Implementing access control mechanisms to restrict access to resources based on user permissions is essential. Only authorized users should be allowed to access specific resources.

Indirect Object References: Instead of using direct references such as primary keys or file names, use indirect references like randomized tokens or hashes that cannot be easily guessed by attackers.

Input Validation: Validate and sanitize all user input to prevent attackers from injecting malicious code into the system.

Secure Data Transmission: Use secure protocols such as HTTPS to ensure secure data transmission between the client and server, to prevent attackers from intercepting and manipulating data.

# Vulnerability Category: Client Hidden Sensitive Data

- Login to the Website using ```qmei```

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image10.png){width=50%}

- Go to Grades

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image6.png){width=50%}

- View Page

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image7.png){width=50%}

- All the ```user-id's``` of all the students are displayed within ```div id ="grade-select"```

- Change the ```style="display"``` to True.

```htm
<div id=\"grade-select\" style=\"display: none;\"\>
<select name=\"user\_id\"\>
<option value=\"38\"\>aabreu\</option\>
<option value=\"44\"\>aburgess\</option\>
<option value=\"39\"\>agabrielson\</option\>
<option value=\"48\"\>asneijders\</option\>
<option value=\"57\"\>clopez\</option\>
<option value=\"51\"\>dfreud\</option\>
<option value=\"20\"\>dhidalgo\</option\>
<option value=\"13\"\>ealbrici\</option\>
<option value=\"37\"\>emasson\</option\>
<option value=\"27\"\>ereynders\</option\>
<option value=\"32\"\>fbabic\</option\>
<option value=\"31\"\>ftrudeau\</option\>
<option value=\"14\"\>gdrake\</option\>
<option value=\"15\"\>gkeller\</option\>
<option value=\"50\"\>gkorrapati\</option\>
<option value=\"30\"\>gradic\</option\>
<option value=\"41\"\>heldridge\</option\>
<option value=\"54\"\>hmullins\</option\>
<option value=\"35\"\>igárdonyi\</option\>
<option value=\"52\"\>itreloar\</option\>
<option value=\"59\"\>jakselsen\</option\>
<option value=\"17\"\>janson\</option\>
<option value=\"25\" selected=\"selected\"\>jtriggs\</option\>
<option value=\"45\"\>khancock\</option\>
<option value=\"43\"\>ksteinsson\</option\>
<option value=\"53\"\>leengman\</option\>
<option value=\"34\"\>lhepburn\</option\>
<option value=\"12\"\>llorenzen\</option\>
<option value=\"56\"\>lphan\</option\>
<option value=\"49\"\>mantal\</option\>
<option value=\"18\"\>mriese\</option\>
<option value=\"22\"\>nbradford\</option\>
<option value=\"42\"\>ofionnagáin\</option\>
<option value=\"21\"\>omaccrumb\</option\>
<option value=\"19\"\>omcneill\</option\>
<option value=\"26\"\>qmei\</option\>
<option value=\"46\"\>sgagnon\</option\>
<option value=\"29\"\>snizzola\</option\>
<option value=\"23\"\>swhitaker\</option\>
<option value=\"16\"\>tnakagawa\</option\>
<option value=\"40\"\>tvasilev\</option\>
<option value=\"24\"\>twägner\</option\>
<option value=\"33\"\>vkaufmann\</option\>
<option value=\"55\"\>vswitzer\</option\>
<option value=\"28\"\>wtamboia\</option\>
<option value=\"36\"\>yllewellyn\</option\>
<option value=\"58\"\>zkovach\</option\>
<option value=\"47\"\>zyap\</option\>
</select\>
<input type=\"submit\" value=\"VIEW GRADES\"\>
</div\>
```

- All users, and ability to view their grade is viewable

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image11.png){width=50%}

## Impact

A client hidden sensitive data attack is a type of cyber attack in which an attacker gains unauthorized access to sensitive data stored on a web applications, or clients environments. 

## Mitigation
Implement encryption: Encryption can be used to secure data that is being sent between the client and server. This ensures that even if the data is intercepted, it cannot be read without the proper decryption key.

Input validation: It is important to validate all input data that is received from clients. This includes hidden fields and cookies. This can be done by checking the data against a set of predefined rules or regular expressions.

Server-side validation: Server-side validation can also be used to validate input data. This involves verifying the data that is received from the client against a set of predefined rules and ensuring that it is safe to process.

Use tokens: Tokens can be used to ensure that data being sent from the client to the server is authentic. Tokens can be generated by the server and sent to the client as a hidden field or cookie. The server can then verify the token when it is received back from the client.

# Vulnerability Category: File-Upload

- Go to login

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image10.png){width=50%}

- Go to Grades

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image6.png){width=50%}

- Select Resubmit

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image7.png){width=50%}

- Upload a file.

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image12.png){width=50%}

- For my example I used a .PHP file.

- Name PHP file hello.pdf.php

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image13.png){width=50%}

- File uploaded successfully

- When the file is viewed the hello world text is shown

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-flag/img/image14.png){width=90%}

## Impact

A file upload attack is a type of cyber attack in which an attacker tries to upload and execute malicious code or files onto a target system through the file upload feature of a website or application. Such an attack can have numerous negative impacts on both the targeted system and its users. Here are some of the most common negative impacts of a file upload attack:

Malware Infection: If an attacker successfully uploads and executes a malicious file on the target system, it can infect the system with malware, causing damage to the system and its data.

Data Theft: A file upload attack can also be used to steal sensitive data from the targeted system. For example, an attacker may upload a script that extracts sensitive data, such as user passwords, credit card numbers, or other personal information.

System Downtime: A successful file upload attack can result in the target system being taken offline or made unavailable to legitimate users. This can cause significant disruption to business operations or services, leading to loss of revenue and reputation.

Legal Liability: A file upload attack can expose an organization to legal liability if sensitive customer data is stolen or if the attack results in financial losses for customers.

Reputational Damage: If a file upload attack is successful, it can damage the reputation of the targeted organization, leading to loss of customer trust and potential business opportunities.

## Mitigation

Limit file types: Restrict the types of files that can be uploaded to the web server. Whitelist file types that are safe and necessary for the web application to function, while blocking all others.

Check file content: Scan the content of the uploaded files to ensure they match the file type and are not corrupted or malicious. Use tools such as antivirus software and content scanning libraries to detect any potential threats.

Sanitize file names: Rename uploaded files to remove any special characters, spaces, or other potentially harmful characters that could be used to execute code or inject malicious commands.

Set file size limits: Define a maximum file size that can be uploaded to the server. This will limit the amount of data that can be sent to the server, reducing the risk of overload or denial of service attacks.

Use secure connections: Require secure connections (HTTPS) for file uploads to ensure that data is encrypted during transmission.

Implement user authentication and authorization: Implement strong user authentication and authorization mechanisms to ensure that only authorized users can upload files to the server.
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

# Vulnerability Category: SQLI Attack

- Go to Login Page

    ![image1](images/media/image1.png){width=50%}
  
  
    

- Open Firefox Developer Tools

- Change the onsubmit parameters to: ```onsubmit=\"return true\"```

```htm
<form id=\"comment-form\" action=\"profile.php?id=26\" method=\"post\"
style=\"margin-top:20px\" onsubmit=\"return
validateCommentForm();\"\>\<textarea rows=\"4\" name=\"comment\"
placeholder=\"Write a comment here\...\"\>\</textarea\>\
<input type=\"submit\" value=\"COMMENT\" style=\"margin-left: auto;
margin-right: auto;\"\> \</form\>
```

- Enter: ``` admin\" OR 1=1\-- ``` without a password

    ![ImgPlaceholder](image3.png){width=50%}

## Impact

XXX

## Mitigation

XXXXXX

# Vulnerability Category: XSS Attack

- Login to the Website using: ```qmei```

    ![ImgPlaceholder](image1.png){width=50%}

- Go to the profile page

    ![ImgPlaceholder](image4.png){width=50%}

- Change the onsubmit parameters to ```onsubmit=\"return true\"```

```htm
<form id=\"comment-form\" action=\"profile.php?id=26\" method=\"post\"
style=\"margin-top:20px\" onsubmit=\"return
validateCommentForm();\"\>\<textarea rows=\"4\" name=\"comment\"
placeholder=\"Write a comment here\...\"\>\</textarea\>\
<input type=\"submit\" value=\"COMMENT\" style=\"margin-left: auto; margin-right: auto;\"\>\</form\>

```

- Add the following to the comment box: ```<scrscriptipt> alert(\"Something\")</script\>```

    ![ImgPlaceholder](image5.png){width=90%}

## Impact

XXX

## Mitigation

XXX

# Vulnerability Category: Insecure Direct Object Reference

- Login to the Website using ```qmei```

    ![ImgPlaceholder](image1.png){width=50%}

- Go to the grades page

    ![ImgPlaceholder](image6.png){width=50%}

- View any submission

    ![ImgPlaceholder](image7.png){width=50%}

- Observe how the url directory is ```/handins/```

    ![ImgPlaceholder](image8.png){width=90%}

- Browse to: ```http://localhost:8888/handins/```

    ![ImgPlaceholder](image9.png){width=50%}

- Another example: ```http://localhost:8888/handouts/```

- All ```/handins/``` can be see no matter if you are logged-in or not

## Impact

XXX

## Mitigation

XXX

# Vulnerability Category: Client Hidden Sensitive Data

- Login to the Website using ```qmei```

    ![ImgPlaceholder](image10.png){width=50%}

- Go to Grades

    ![ImgPlaceholder](image6.png){width=50%}

- View Page

    ![ImgPlaceholder](image7.png){width=50%}

- All the ```user-id's``` of all the students are displayed within ```div id ="grade-select"```

- Change the ```style=\"display\"``` to True.

```htm
<div id=\"grade-select\" style=\"display: none;\"\>
<select name=\"user\_id\"\>
<option value=\"38\"\>aabreu\</option\>
<option value=\"44\"\>aburgess\</option\>
<option value=\"39\"\>agabrielson\</option\>
<option value=\"48\"\>asneijders\</option\>
<option value=\"57\"\>clópez\</option\>
<option value=\"51\"\>dfreud\</option\>
<option value=\"20\"\>dhidalgo\</option\>
<option value=\"13\"\>ealbrici\</option\>
<option value=\"37\"\>emasson\</option\>
<option value=\"27\"\>ereynders\</option\>
<option value=\"32\"\>fbabić\</option\>
<option value=\"31\"\>ftrudeau\</option\>
<option value=\"14\"\>gdrake\</option\>
<option value=\"15\"\>gkeller\</option\>
<option value=\"50\"\>gkorrapati\</option\>
<option value=\"30\"\>gradić\</option\>
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
<option value=\"58\"\>zkovách\</option\>
<option value=\"47\"\>zyap\</option\>
</select\>
<input type=\"submit\" value=\"VIEW GRADES\"\>
</div\>
```

- All users, and ability to view their grade is viewable

    ![ImgPlaceholder](image11.png){width=50%}

## Impact

XXX

## Mitigation

XXX

# Vulnerability Category: File-Upload

- Go to login

    ![ImgPlaceholder](image10.png){width=50%}

- Go to Grades

    ![ImgPlaceholder](image6.png){width=50%}

- Select Resubmit

    ![ImgPlaceholder](image7.png){width=50%}

- Upload a file.

    ![ImgPlaceholder](image12.png){width=50%}

- For my example I used a .PHP file.

- Name PHP file hello.pdf.php

    ![ImgPlaceholder](image13.png){width=50%}

- File uploaded successfully

- When the file is viewed the hello world text is shown

    ![ImgPlaceholder](image14.png){width=50%}

## Impact

XXX

## Mitigation

XXX
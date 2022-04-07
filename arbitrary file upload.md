# Arbitrary file upload / CVE-2022-28052

> 1. cn/roothub/web/front/CommonController.java:35<br>
At "/common/upload" api, parameter "customPath" is used as 2nd param of storageService.store();<br>
![image](https://user-images.githubusercontent.com/9525971/159516937-88f5a23f-fed6-42b1-bac2-675f37c4e6f6.png)

<br><br>
> 2. Then the "path" is concatenated to storageProperties.getUploadFiledir(), finally passed to path.resolve();<br>
![image](https://user-images.githubusercontent.com/9525971/159517821-df09bbbc-b1ce-42d6-897c-38cbaa83db75.png)<br>

<br><br>
> 3. In FileNameUtil.getFileName(), it just simply renames the basename of file with random uuid and concatenated the suffix;<br>
![image](https://user-images.githubusercontent.com/9525971/159519333-77f7b610-c87f-418c-8d06-a6e04097be92.png)

<br><br>
> 4. So we only need to <br>
    - tamper the suffix of an originally valid file to bypass the front-end validation<br>
    - construct the customPath param in post body params which includes "../" to complete path traversal

<br><br>
> 5. Final payload:<br>
![image](https://user-images.githubusercontent.com/9525971/159520998-5591227f-b74e-4271-8bb3-419da38a1236.png)

<br><br>
> 6. Here we used /etc/bash_completion.d to add an shell script, so the RCE will be triggered automatically each time the victim logs into bash, which is super ez to achieve.<br>
![image](https://user-images.githubusercontent.com/9525971/159522138-e92ac3d0-b85b-4afa-b40c-2a2f0205f200.png)


<br><br>
> 7. After the login, we can see that the code had gotten executed.<br>
![image](https://user-images.githubusercontent.com/9525971/159522100-25d84416-39c1-4697-b904-387714c72427.png)

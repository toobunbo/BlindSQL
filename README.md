# BlindSQL
## Post này sẽ giải thích nhập môn về cái SQL injection, cụ thể là Blind
-  Ở chall 15 của natas có đề cập đến phương thức khai thác này ![natas15](https://learnhacking.io/content/images/wordpress/2021/11/natas-level15-source-code.png)
-  Ý tưởng chính sẽ là truyền "username=natas16\" AND substring(password,1,count) = 'c' -- " vào payload để khai thác SQLinjection. Do mật khẩu có 64 ký tự (a-z, A-Z, 0-9) nên script khai thác trông nó sẽ như này
 [image](https://github.com/user-attachments/assets/c9afbb5d-d017-428d-aa65-c373f4070950)
 

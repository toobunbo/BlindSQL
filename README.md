# BlindSQL
## Post này sẽ giải thích nhập môn về cái SQL injection, cụ thể là Blind
-  Ở chall 15 của natas có đề cập đến phương thức khai thác này ![natas15](https://learnhacking.io/content/images/wordpress/2021/11/natas-level15-source-code.png)
-  Ý tưởng chính sẽ là truyền - "username=natas16\" AND substring(password,1,count) = 'c' -- " vào payload để khai thác SQLinjection. Do mật khẩu có 64 ký tự (a-z, A-Z, 0-9) nên script khai thác trông nó sẽ như này
 [image](https://github.com/user-attachments/assets/c9afbb5d-d017-428d-aa65-c373f4070950)
- Nhìn sơ qua, dù ngu ta cũng có thể thấy để dựng kịch bảng này cần 3 yếu tố chính
1. Độ dài của mk
2. Valid character
3. Server trả về dấu hiệu đúng nếu như khớp mk (cái này không quan trọng vì có thể chơi bằng Time base --dễ quá nên không đề cập).
- Rồi, vậy khi gặp một trường hợp mất dạy thì sau :🙂. Kiểu
1. Không cho biết độ dài mật khẩu (for sure tất nhiên r)
2. Mật khẩu viết bằng tiếng Hàn :))).
3. Vào việc
## Đây là nội dung chính của cái post này (đọc từ đây nghe mấy con gà)
- Lấy ý tưởng từ một chall của DreamHackm ta có một server nho nhỏ cần khai thác như sau:
![image](https://github.com/user-attachments/assets/e78c22f1-ff51-4c68-bb68-f87b72997b74)
- Ta chỉ được biết mật khẩu được viết bằng ASCII hoặc tiếng Hàn (thì làm như nào)
## Write -up
### Xác định độ dài mật khẩu
### Phân tách mật khẩu thành Bit (không rõ cho lắm)
### Dò mật khẩu bằng Bit
### Dịch ngược lại thành mật khẩu ký tự



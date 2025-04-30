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
`import os
from flask import Flask, request, render_template_string
from flask_mysqldb import MySQL

app = Flask(__name__)
app.config['MYSQL_HOST'] = os.environ.get('MYSQL_HOST', 'localhost')
app.config['MYSQL_USER'] = os.environ.get('MYSQL_USER', 'user')
app.config['MYSQL_PASSWORD'] = os.environ.get('MYSQL_PASSWORD', 'pass')
app.config['MYSQL_DB'] = os.environ.get('MYSQL_DB', 'user_db')
mysql = MySQL(app)

template ='''
<pre style="font-size:200%">SELECT * FROM users WHERE uid='{{uid}}';</pre><hr/>
<form>
    <input tyupe='text' name='uid' placeholder='uid'>
    <input type='submit' value='submit'>
</form>
{% if nrows == 1%}
    <pre style="font-size:150%">user "{{uid}}" exists.</pre>
{% endif %}
'''

@app.route('/', methods=['GET'])
def index():
    uid = request.args.get('uid', '')
    nrows = 0

    if uid:
        cur = mysql.connection.cursor()
        nrows = cur.execute(f"SELECT * FROM users WHERE uid='{uid}';")

    return render_template_string(template, uid=uid, nrows=nrows)


if __name__ == '__main__':
    app.run(host='0.0.0.0')`

# Lỗ hổng CSRF ( CROSS SITE REQUEST FORGERY)

## LAB: SAMESITE LAX BYPASS VIA COOKIE REFRESH  

B1: Đăng nhập vào tài khoản wiener:peter <br>
B2: Thay đổi email => quan sát http request trong Burp <br>
![image](https://github.com/user-attachments/assets/49cbd368-7898-4e8b-8a6d-3bf41916e5a7)  
![image](https://github.com/user-attachments/assets/23b0f803-75b3-474b-b345-550b218a2bc2) <br>
B3: Quan sát yêu cầu POST /my-account/change-email không có tham số k thể doán trước => Nguy cơ tấn công CSRF <br>
B4: 

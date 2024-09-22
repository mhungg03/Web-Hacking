# Lỗ hổng CSRF ( CROSS SITE REQUEST FORGERY)

## LAB: SAMESITE LAX BYPASS VIA COOKIE REFRESH  

B1: Đăng nhập vào tài khoản wiener:peter <br>
B2: Thay đổi email => quan sát http request trong Burp <br>
![image](https://github.com/user-attachments/assets/49cbd368-7898-4e8b-8a6d-3bf41916e5a7)  
![image](https://github.com/user-attachments/assets/23b0f803-75b3-474b-b345-550b218a2bc2) <br>
B3: Quan sát yêu cầu POST /my-account/change-email không có tham số k thể doán trước => Nguy cơ tấn công CSRF <br>
B4: Quan sát yêu cầu GET oauth-callback.. thấy web không thiết lập cookie samesite nào => mặc định là LAX  
![image](https://github.com/user-attachments/assets/a4784ecd-4c98-4bde-bb9c-3dbf6630a009)  
B5: Hacker tạo 1 form HTML như sau để thử khai thác lỗ hổng  
![image](https://github.com/user-attachments/assets/c9c6c125-028b-4648-bdd1-0679cbce8fe8)  
B6: Lưu trữ đoạn script và xem khai thác tuy nhiên nếu quá 2p cuộc tấn công sẽ thát bại, lăp lại bước đăng nhập và thử lại  
![image](https://github.com/user-attachments/assets/948639e5-4f34-40cb-bcb2-411a8cd9c61c)  
B7: 



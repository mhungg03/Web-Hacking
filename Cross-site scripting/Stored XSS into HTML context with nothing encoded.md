**B1**: Theo mô tả của lab thì XSS xuất hiện ở chức năng comment, ta thử sẽ bấm chọn 1 blog bất kì và comment  
![image](https://github.com/user-attachments/assets/11ee1649-688c-4977-bca6-a6787a8335e4)  
Khi bấm send thì cmt sẽ ngay lập tức được hiện ra ở bài post
![image](https://github.com/user-attachments/assets/6792c489-626c-4b41-af32-675a48029c6b)    
**B2**: Để kiểm tra xem trang web có encode HTML tag hay không ta thử cmt  
<h1>Blah</h1>  

![image](https://github.com/user-attachments/assets/44fd601d-9f2d-42e9-85c0-47083065cdd1)    
![image](https://github.com/user-attachments/assets/4fff0e79-94d6-4a19-b257-9026b9f7853d)    
Blah đã thành tiêu đề H1, do đó trang web không hề encode HTML tag
**B3**: Nhập <script>alert('xss')</script> để tấn công Stored XSS  
![image](https://github.com/user-attachments/assets/11e6e60b-1a19-4b74-a01f-e09d392e1d24)






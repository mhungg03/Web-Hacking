* Bài lab này có xss ở mục tìm kiếm sử dụng Angular Js, ta thử nhập payload khai thác xss vào `<script>alert(1)</script>`  
![image](https://github.com/user-attachments/assets/6c89b6f2-9bc2-4192-a2cc-f8e8dad4c0e5)  
Dấu ngoặc nhọn đã bị encode nên js không thể thực thi  
* Quan sát source code thấy
  ![image](https://github.com/user-attachments/assets/f04a4b8e-3b93-487d-8283-70d51a98c18a)
  Web đang dùng angular js được bọc trong ng-app cho phép thực thi js bên trong {{ }}
* Thử nhập `{{ alert(1) }}`
  ![image](https://github.com/user-attachments/assets/19d8b149-323e-46c1-b261-364a16c4c3fb)
* Không khai thác được, payload vẫn đang nằm trong dấu ' '
* Dùng payload sau để truy cập function constructor tạo ra 1 hàm mới
  `{{$on.constructor('alert(1)')()}}`
  
 pop up alert đã xuất hiện





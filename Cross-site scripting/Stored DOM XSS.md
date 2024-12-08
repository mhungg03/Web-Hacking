**B1**: Theo mô tả của bài lab thì có lỗ hổng ở phần cmt, ta cmt vào và check request trong burp suite  
![image](https://github.com/user-attachments/assets/1a9b1309-cdba-47f2-b287-abd71bbdced8)  
Quan sát thấy file js này thực hiện chức năng loadcomment  
**B2**: View source code   
![image](https://github.com/user-attachments/assets/ac9da48b-dd87-4a53-8f14-a050804c2424)  
Hàm escapeHTML sử dụng replace để mã hóa > và < nhưng replace chỉ thay thế được kí tự đầu tiên, có nghĩa là kí tự thứ 2 sẽ không được mã hóa :V  
**B3**: Thử payload sau để khai thác xss `<h1><img src=1 onerror=alert(1)>`
![image](https://github.com/user-attachments/assets/1b5c4568-1a86-4d6d-9745-9f39483f56d5)



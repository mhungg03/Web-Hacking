* Theo mô tả của lab thì có vuln ở homepage, mở devtool lên và kiểm tra
  ![image](https://github.com/user-attachments/assets/75bf63da-5b82-45d2-ab2e-b66844b310e8)
* Phân tích code một chút
  Jquery sẽ lấy tất cả những class có tên là blog list, chọn các thẻ h2 có chứa nội dung là url sau dấu #, mỗi lần nội dung thay đổi thì 
  func sẽ được gọi và thực thi do có sự kiện hashchange.
* https://bugs.jquery.com/ticket/9521/ vào link này tìm kiếm thì ra được thông tin là thư viện jquery phiên bản này gặp lỗi ở chức năng 
 location.hash, thay vì chỉ cho phép một css selector nó có thể tạo được HTML
* Thử thêm payload sau vào url `<img src=1 onerror=print()>` ngay lập tức màn hình đã hiện chế độ print
  ![image](https://github.com/user-attachments/assets/1be46039-29a1-456c-9e30-6bb4d0196ee2)
* Tuy nhiên không thể gửi cho người dùng link này vì chỉ khi giá trị sau # thay đổi thì mới kích hoạt được javascript,để giải quyết ta sẽ sử dụng thẻ iframe để nhúng trang web với url trước dấu #, sau đó nối với payload của chúng ta
  `<iframe src="https://YOUR-LAB-ID.web-security-academy.net/#" onload="this.src+='<img src=x onerror=print()>'"></iframe>`
* Chuyển đến exploit server và gửi cho người dùng link trên 
  



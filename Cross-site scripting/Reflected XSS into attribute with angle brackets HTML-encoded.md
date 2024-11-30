* Mô tả của bài lab cho thấy có lỗ hổng ở mục search, ta nhập 1 payload vào và kiểm tra
  `<script>alert(1)</script>`
* Sau khi view page source ra thì thấy dấu ngoặc nhọn đã bị encode từ phía backend
  ![image](https://github.com/user-attachments/assets/d7af73ff-1735-4e70-9535-5bfa15a2b57f)
* Quan sát thẻ input, ta có thể dùng payload sau để thử thoát khỏi dấu nháy
  `hehe" onmouseover="alert(1)`
  ![image](https://github.com/user-attachments/assets/daaeb841-4e7e-4bf4-86c1-e553ea4d95ef)



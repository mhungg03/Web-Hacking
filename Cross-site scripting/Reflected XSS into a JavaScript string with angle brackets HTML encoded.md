* Theo mô tả của bài lab, xss ở trong chức năng truy vấn tìm kiếm nên ta nhập 1 chuỗi vào ô tìm kiếm `hehe`
* View source code ra xem
  ![image](https://github.com/user-attachments/assets/18cca79e-b10f-4184-9ddf-9f659157d24f)
* Vì đang ở trong thẻ script nên ta thử thêm payload sau để thoát khỏi chuỗi `hehe' + alert(1) + '`
* Kiểm tra source code thấy đã chèn đc js vào DOM
  ![image](https://github.com/user-attachments/assets/8b9a63e9-b43f-45ee-aae4-9e854aabe63b)



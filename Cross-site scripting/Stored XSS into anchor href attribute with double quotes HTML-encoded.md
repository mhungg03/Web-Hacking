* Theo mô tả của bài lab thì nó bị xss ở phần cmt nên ta vào post 1 cmt để check
* Sau khi post cmt lên ta được như sau
  ![image](https://github.com/user-attachments/assets/357f63e4-82c5-434b-a84a-7c9eda2a9a8e)
* View source code lên để xem
  ![image](https://github.com/user-attachments/assets/22604e9b-3151-4980-81a1-5a63aa80400c)
  Đoạn mã này cho thấy rằng website chúng ta nhập vào sẽ được thêm vào href
* Dùng payload sau để chèn javascript vào href
  `javascript:alert(1)`
* Ngay khi chúng ta bấm vào tên tác giả, xss đã xuất hiện
  ![image](https://github.com/user-attachments/assets/196a07da-2833-4a44-a8b6-ac527190675b)




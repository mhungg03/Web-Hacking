* Theo mô tả của lab thì có vuln ở submit feedback page nên ta thử vào khám phá xem
  ![image](https://github.com/user-attachments/assets/eeba4828-8728-4ba9-808b-62e1c40b69c6)

* Quan sát url thấy có returnpath/ và ở cuối page có chữ back, đoán được rằng khi bấm back thì sẽ return về trang chủ
* Inspect code lên xem
  ![image](https://github.com/user-attachments/assets/f2465fa7-f793-4953-89d7-9e3aa200fea8)
* Phân tích code ta có thể thấy web dùng jquery để lấy thẻ html có id là backlink, sau đó thêm attribute href với giá trị là những gì mà ta nhập trên url
* Vì trong href ta có thể chạy được javascript nên ta sẽ thử thêm payload như sau `javascript:alert(document.cookie)`
  ![image](https://github.com/user-attachments/assets/66a0bad9-1216-4d65-9833-a20929fee7a7)


  


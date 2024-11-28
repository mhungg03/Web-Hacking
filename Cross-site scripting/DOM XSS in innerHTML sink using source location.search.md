**B1**: Ta thử test 1 thẻ html vào ô tìm kiếm `<h1>test</h1>`  
![image](https://github.com/user-attachments/assets/f39a001a-dd3a-4627-8b75-f47c55a446a1)  
Website không hề encode thẻ html nên ta có thể thấy html tag đã được thêm vào dom  
**B2**: Quan sát thấy những gì chúng ta search đang nằm trong thẻ span, thử escape thẻ span xem  
`<span><script>alert(1)</script>`  
![image](https://github.com/user-attachments/assets/690787d7-b46c-44f6-8c6a-a17abf17b57f)  
Chúng ta vẫn nằm trong thẻ span :) thử tìm kiếm file js xem  
![image](https://github.com/user-attachments/assets/ab806143-9d23-401b-b0f0-e2eccff04eb0)
**B3**: Đọc file js ta có thể thấy web đang sử dụng innerhtml để thêm nội dung từ query  
=> sử dụng payload sau để XSS `<img src=1 onerror="alert(1)">  
![image](https://github.com/user-attachments/assets/16a1b4b5-8c5d-4da9-a21d-de306dcd793e)  
![image](https://github.com/user-attachments/assets/9d797ae2-8d1d-41ec-a485-9f62b54ae66b)  
=> Thẻ img đã được thêm vào DOM do đó kích hoạt sự kiện onerror do source ảnh bị sai 







**B1**: Gửi 1 chuỗi bất kì và vào burpsuite bắt request  
![image](https://github.com/user-attachments/assets/80e0da9a-90d7-4201-a904-d27b92eb3d60)  
Quan sát thấy có 1 file js này được trả về, view source ra quan sát  
**B2**: Quan sát đoạn code và thấy có sử dụng hàm eval() để chuyển string json nhận được từ respontext về đối tượng  
![image](https://github.com/user-attachments/assets/76070477-8a4a-4e3b-9c58-2501fcdf345a)  
eval() có lỗ hổng bảo mật cho phép chạy javascript trong chuỗi nên ta phải chèn được js vào searchTerm  
**B3**: Đây là searchResultObj mà ta nhận được từ server  
![image](https://github.com/user-attachments/assets/1fae38d6-4e3e-451e-90db-8f0a46416e7c)  
Chúng ta phải chèn js vào searchTerm  
**B4**: Sử dụng payload sau để chèn js vào chuỗi searchTerm  
![image](https://github.com/user-attachments/assets/86d8dd33-ca64-4c4c-bb04-c56a0ff7cb35)



**B1**: Theo mô tả của bài lab thì website này bị vuln ở chức năng tracking search do sử dụng document.write(), ta thử nhập vào ô tìm kiếm một thẻ html xem nó có encode không `<h1>meow</h1>`  
![image](https://github.com/user-attachments/assets/fedb4eff-d55c-4818-a752-1b165df32ea6)  
![image](https://github.com/user-attachments/assets/64249c22-69ce-441d-a992-c2853bb7f779)  
=> website đã mã hóa html tag  
**B2**: Inspect source code và tìm được 1 đoạn mã javascript  
![image](https://github.com/user-attachments/assets/be761d1d-0181-427b-85f8-153c7840dc9f)  
Ta cùng phân tích đoạn code trên  
`window.location.search` sẽ trả về chuỗi truy vấn của url sau dấu ?  
`newURLSearchParams` sẽ tạo một đối tượng mới để lấy giá trị từ chuỗi truy vấn  
`.get('search')` lấy giá trị tham số search từ chuỗi truy vấn, khi có truy vấn thì sẽ kích hoạt document.write và tạo ra 1 thẻ img với tracking gif được nối cùng giá trị của biến query  
**B3**: Quan sát thẻ img sau  
![image](https://github.com/user-attachments/assets/e329b528-81fb-4425-a36f-e4cc88c62dd9)  
Ta có thể dùng thuộc tính onload để kích hoạt hàm js khi nội dung trong thẻ svg được tải  
payload như sau `"><svg onload="alert(1)">`  
![image](https://github.com/user-attachments/assets/0477b1ad-febc-4e21-92d0-a395247168a5)  
![image](https://github.com/user-attachments/assets/a7e0881a-33be-4754-9552-b493ab4acae2)  
hoặc có thể dùng payload đơn giản hơn là `"onload="alert(1)`











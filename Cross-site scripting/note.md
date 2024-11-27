> ### Cross-site scripting là gì ?
Cross-site scripting (còn được gọi là XSS) là một lỗ hổng bảo mật web cho phép kẻ tấn công xâm phạm các tương tác mà người dùng có với một ứng dụng dễ bị tấn công. Nó cho phép kẻ tấn công lách chính sách cùng nguồn gốc, được thiết kế để tách biệt các trang web khác nhau với nhau. Các lỗ hổng cross-site scripting thường cho phép kẻ tấn công ngụy trang thành người dùng nạn nhân, thực hiện bất kỳ hành động nào mà người dùng có thể thực hiện và truy cập bất kỳ dữ liệu nào của người dùng. Nếu người dùng nạn nhân có quyền truy cập đặc quyền trong ứng dụng, thì kẻ tấn công có thể giành được quyền kiểm soát hoàn toàn đối với tất cả các chức năng và dữ liệu của ứng dụng.
> ### XSS hoạt động như thế nào ?
Cross-site scripting hoạt động bằng cách thao túng một trang web dễ bị tấn công để trả về JavaScript độc hại cho người dùng. Khi mã độc hại thực thi bên trong trình duyệt của nạn nhân, kẻ tấn công có thể xâm phạm hoàn toàn tương tác của họ với ứng dụng.
![image](https://github.com/user-attachments/assets/23227aa5-420c-451d-be6b-f482c89f9b45)
> ### Tác động của XSS
Tác động thực tế của một cuộc tấn công XSS thường phụ thuộc vào bản chất của ứng dụng, chức năng và dữ liệu của ứng dụng, cũng như trạng thái của người dùng bị xâm phạm. Ví dụ:

* Trong ứng dụng brochureware, nơi tất cả người dùng đều ẩn danh và mọi thông tin đều được công khai, tác động thường sẽ rất nhỏ.
* Trong ứng dụng lưu trữ dữ liệu nhạy cảm, chẳng hạn như giao dịch ngân hàng, email hoặc hồ sơ chăm sóc sức khỏe, tác động thường sẽ rất nghiêm trọng.
* Nếu người dùng bị xâm phạm có quyền cao hơn trong ứng dụng, thì tác động thường sẽ rất nghiêm trọng, cho phép kẻ tấn công kiểm soát hoàn toàn ứng dụng 
  dễ bị tấn công và xâm phạm tất cả người dùng và dữ liệu của họ.
> ### Cách tìm và kiểm tra lỗ hổng XSS
Phần lớn các lỗ hổng XSS có thể được tìm thấy nhanh chóng và đáng tin cậy bằng trình quét lỗ hổng web của Burp Suite .

Kiểm tra thủ công đối với XSS phản ánh và lưu trữ thường bao gồm việc gửi một số đầu vào duy nhất đơn giản (chẳng hạn như một chuỗi chữ số ngắn) vào mọi điểm vào trong ứng dụng, xác định mọi vị trí mà đầu vào đã gửi được trả về trong phản hồi HTTP và kiểm tra từng vị trí riêng lẻ để xác định xem đầu vào được chế tạo phù hợp có thể được sử dụng để thực thi JavaScript tùy ý hay không. Theo cách này, bạn có thể xác định bối cảnh mà XSS xảy ra và chọn một tải trọng phù hợp để khai thác nó.

Kiểm tra thủ công đối với XSS dựa trên DOM phát sinh từ các tham số URL bao gồm một quy trình tương tự: đặt một số đầu vào duy nhất đơn giản vào tham số, sử dụng các công cụ dành cho nhà phát triển của trình duyệt để tìm kiếm DOM cho đầu vào này và kiểm tra từng vị trí để xác định xem nó có thể khai thác được hay không. Tuy nhiên, các loại DOM XSS khác khó phát hiện hơn. Để tìm các lỗ hổng dựa trên DOM trong đầu vào không dựa trên URL (như document.cookie) hoặc các bồn chứa không dựa trên HTML (như setTimeout), không có cách nào thay thế cho việc xem xét mã JavaScript, có thể cực kỳ tốn thời gian. Trình quét lỗ hổng web của Burp Suite kết hợp phân tích tĩnh và động của JavaScript để tự động phát hiện các lỗ hổng dựa trên DOM một cách đáng tin cậy.  
> ### 1.Reflected XSS
Tấn công chéo trang web phản chiếu (hay XSS) xảy ra khi một ứng dụng nhận dữ liệu trong yêu cầu HTTP và đưa dữ liệu đó vào phản hồi ngay lập tức theo cách không an toàn.

Giả sử một trang web có chức năng tìm kiếm nhận từ khóa tìm kiếm do người dùng cung cấp trong tham số URL:
`https://insecure-website.com/search?term=gift`  
Ứng dụng sẽ lặp lại thuật ngữ tìm kiếm được cung cấp trong phản hồi cho URL này:
`<p>You searched for: gift</p>`
Giả sử ứng dụng không thực hiện bất kỳ xử lý dữ liệu nào khác, kẻ tấn công có thể xây dựng một cuộc tấn công như thế này:
`https://insecure-website.com/search?term=<script>/*+Bad+stuff+here...+*/</script>`
URL này sẽ cho kết quả phản hồi như sau:
`<p>You searched for: <script>/* Bad stuff here... */</script></p>`
Nếu người dùng ứng dụng khác yêu cầu URL của kẻ tấn công, thì tập lệnh do kẻ tấn công cung cấp sẽ được thực thi trên trình duyệt của người dùng nạn nhân, trong bối cảnh phiên làm việc của họ với ứng dụng.  
> ### Ảnh hưởng của cuộc tấn công XSS Reflected
Nếu kẻ tấn công có thể kiểm soát một tập lệnh được thực thi trong trình duyệt của nạn nhân, thì thông thường chúng có thể xâm phạm hoàn toàn người dùng đó. Trong số những thứ khác, kẻ tấn công có thể:

Thực hiện bất kỳ hành động nào trong ứng dụng mà người dùng có thể thực hiện.
* Xem bất kỳ thông tin nào mà người dùng có thể xem.
* Sửa đổi bất kỳ thông tin nào mà người dùng có thể sửa đổi.
* Khởi tạo tương tác với những người dùng ứng dụng khác, bao gồm các cuộc tấn công độc hại, có vẻ như xuất phát từ người dùng nạn nhân ban đầu.
Có nhiều cách khác nhau mà kẻ tấn công có thể dùng để dụ dỗ người dùng nạn nhân đưa ra yêu cầu mà chúng kiểm soát, để thực hiện một cuộc tấn công XSS phản chiếu. Những cách này bao gồm đặt liên kết trên một trang web do kẻ tấn công kiểm soát, hoặc trên một trang web khác cho phép tạo nội dung, hoặc bằng cách gửi liên kết trong email, tweet hoặc tin nhắn khác. Cuộc tấn công có thể nhắm trực tiếp vào một người dùng đã biết hoặc có thể là một cuộc tấn công bừa bãi vào bất kỳ người dùng nào của ứng dụng.

Nhu cầu về một cơ chế phân phối bên ngoài cho cuộc tấn công có nghĩa là tác động của XSS phản ánh thường ít nghiêm trọng hơn XSS được lưu trữ , trong đó một cuộc tấn công độc lập có thể được phân phối trong chính ứng dụng dễ bị tấn công.
> ### Các loại Reflected XSS
Có nhiều loại kịch bản chéo trang phản chiếu khác nhau. Vị trí của dữ liệu phản chiếu trong phản hồi của ứng dụng xác định loại tải trọng nào cần thiết để khai thác nó và cũng có thể ảnh hưởng đến tác động của lỗ hổng.

Ngoài ra, nếu ứng dụng thực hiện bất kỳ xác thực hoặc xử lý nào khác trên dữ liệu đã gửi trước khi dữ liệu đó được phản ánh, điều này thường sẽ ảnh hưởng đến loại tải trọng XSS cần thiết.
> ### Làm thế nào để tìm và kiểm tra XSS Reflected ?
Phần lớn các lỗ hổng tấn công chéo trang web có thể được tìm thấy nhanh chóng và đáng tin cậy bằng trình quét lỗ hổng web của Burp Suite .

Kiểm tra lỗ hổng XSS phản ánh theo cách thủ công bao gồm các bước sau:

* Kiểm tra mọi điểm vào. Kiểm tra riêng từng điểm vào để tìm dữ liệu trong các yêu cầu HTTP của ứng dụng. Điều này bao gồm các tham số hoặc dữ liệu khác trong chuỗi truy vấn URL và nội dung tin nhắn, và đường dẫn tệp URL. Nó cũng bao gồm các tiêu đề HTTP, mặc dù hành vi giống như XSS chỉ có thể được kích hoạt thông qua một số tiêu đề HTTP nhất định có thể không khai thác được trong thực tế.
* Gửi các giá trị chữ số ngẫu nhiên. Đối với mỗi điểm nhập, hãy gửi một giá trị ngẫu nhiên duy nhất và xác định xem giá trị đó có được phản ánh trong phản hồi hay không. Giá trị phải được thiết kế để tồn tại trong hầu hết các xác thực đầu vào, do đó cần phải khá ngắn và chỉ chứa các ký tự chữ số. Nhưng nó cần phải đủ dài để làm cho các kết quả trùng khớp ngẫu nhiên trong phản hồi trở nên rất khó xảy ra. Giá trị chữ số ngẫu nhiên khoảng 8 ký tự thường là lý tưởng. Bạn có thể sử dụng các tải trọng số của Burp Intruder với các giá trị hex được tạo ngẫu nhiên để tạo ra các giá trị ngẫu nhiên phù hợp. Và bạn có thể sử dụng các cài đặt tải trọng grep của Burp Intruder để tự động đánh dấu các phản hồi có chứa giá trị đã gửi.
* Xác định ngữ cảnh phản chiếu. Đối với mỗi vị trí trong phản hồi mà giá trị ngẫu nhiên được phản chiếu, hãy xác định ngữ cảnh của nó. Có thể là trong văn bản giữa các thẻ HTML, trong thuộc tính thẻ có thể được trích dẫn, trong chuỗi JavaScript, v.v.
* Kiểm tra tải trọng ứng viên. Dựa trên ngữ cảnh của phản xạ, hãy kiểm tra tải trọng XSS ứng viên ban đầu sẽ kích hoạt thực thi JavaScript nếu nó được phản xạ không sửa đổi trong phản hồi. Cách dễ nhất để kiểm tra tải trọng là gửi yêu cầu đến Burp Repeater , sửa đổi yêu cầu để chèn tải trọng ứng viên, đưa ra yêu cầu, sau đó xem lại phản hồi để xem tải trọng có hoạt động không. Một cách hiệu quả để làm việc là để lại giá trị ngẫu nhiên ban đầu trong yêu cầu và đặt tải trọng XSS ứng viên trước hoặc sau nó. Sau đó, đặt giá trị ngẫu nhiên làm thuật ngữ tìm kiếm trong chế độ xem phản hồi của Burp Repeater. Burp sẽ làm nổi bật từng vị trí mà thuật ngữ tìm kiếm xuất hiện, cho phép bạn nhanh chóng xác định vị trí phản xạ.
* Kiểm tra các tải trọng thay thế. Nếu tải trọng XSS ứng viên đã bị ứng dụng sửa đổi hoặc bị chặn hoàn toàn, thì bạn sẽ cần kiểm tra các tải trọng và kỹ thuật thay thế có thể cung cấp một cuộc tấn công XSS đang hoạt động dựa trên bối cảnh của phản xạ và loại xác thực đầu vào đang được thực hiện. Để biết thêm chi tiết, hãy xem bối cảnh tập lệnh chéo trang
* Kiểm tra cuộc tấn công trong trình duyệt. Cuối cùng, nếu bạn thành công trong việc tìm ra một tải trọng có vẻ hoạt động trong Burp Repeater, hãy chuyển cuộc tấn công sang một trình duyệt thực (bằng cách dán URL vào thanh địa chỉ hoặc bằng cách sửa đổi yêu cầu trong chế độ xem chặn của Burp Proxy và xem JavaScript được đưa vào có thực sự được thực thi hay không. Thông thường, tốt nhất là thực thi một số JavaScript đơn giản như alert(document.domain)sẽ kích hoạt một cửa sổ bật lên có thể nhìn thấy trong trình duyệt nếu cuộc tấn công thành công.

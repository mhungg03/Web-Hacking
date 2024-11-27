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
There are many different varieties of reflected cross-site scripting. The location of the reflected data within the application's response determines what type of payload is required to exploit it and might also affect the impact of the vulnerability.

In addition, if the application performs any validation or other processing on the submitted data before it is reflected, this will generally affect what kind of XSS payload is needed.
> ### Làm thế nào để tìm và kiểm tra XSS Reflected ?
The vast majority of reflected cross-site scripting vulnerabilities can be found quickly and reliably using Burp Suite's web vulnerability scanner.

Testing for reflected XSS vulnerabilities manually involves the following steps:

* Test every entry point. Test separately every entry point for data within the application's HTTP requests. This includes parameters or other data within the URL query string and message body, and the URL file path. It also includes HTTP headers, although XSS-like behavior that can only be triggered via certain HTTP headers may not be exploitable in practice.
* Submit random alphanumeric values. For each entry point, submit a unique random value and determine whether the value is reflected in the response. The value should be designed to survive most input validation, so needs to be fairly short and contain only alphanumeric characters. But it needs to be long enough to make accidental matches within the response highly unlikely. A random alphanumeric value of around 8 characters is normally ideal. You can use Burp Intruder's number payloads with randomly generated hex values to generate suitable random values. And you can use Burp Intruder's grep payloads settings to automatically flag responses that contain the submitted value.
* Determine the reflection context. For each location within the response where the random value is reflected, determine its context. This might be in text between HTML tags, within a tag attribute which might be quoted, within a JavaScript string, etc.
* Test a candidate payload. Based on the context of the reflection, test an initial candidate XSS payload that will trigger JavaScript execution if it is reflected unmodified within the response. The easiest way to test payloads is to send the request to Burp Repeater, modify the request to insert the candidate payload, issue the request, and then review the response to see if the payload worked. An efficient way to work is to leave the original random value in the request and place the candidate XSS payload before or after it. Then set the random value as the search term in Burp Repeater's response view. Burp will highlight each location where the search term appears, letting you quickly locate the reflection.
* Test alternative payloads. If the candidate XSS payload was modified by the application, or blocked altogether, then you will need to test alternative payloads and techniques that might deliver a working XSS attack based on the context of the reflection and the type of input validation that is being performed. For more details, see cross-site scripting contexts
* Test the attack in a browser. Finally, if you succeed in finding a payload that appears to work within Burp Repeater, transfer the attack to a real browser (by pasting the URL into the address bar, or by modifying the request in Burp Proxy's intercept view, and see if the injected JavaScript is indeed executed. Often, it is best to execute some simple JavaScript like alert(document.domain) which will trigger a visible popup within the browser if the attack succeeds.

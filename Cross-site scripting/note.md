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
`https://insecure-website.com/search?term=gift`  </br>
Ứng dụng sẽ lặp lại thuật ngữ tìm kiếm được cung cấp trong phản hồi cho URL này:<br>
`<p>You searched for: gift</p>`<br>
Giả sử ứng dụng không thực hiện bất kỳ xử lý dữ liệu nào khác, kẻ tấn công có thể xây dựng một cuộc tấn công như thế này:<br>
`https://insecure-website.com/search?term=<script>/*+Bad+stuff+here...+*/</script>`<br>
URL này sẽ cho kết quả phản hồi như sau:
`<p>You searched for: <script>/* Bad stuff here... */</script></p>`<br>
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

> ### 2. Stored XSS
Lỗi mã hóa tập lệnh chéo trang được lưu trữ (còn gọi là XSS bậc hai hoặc XSS dai dẳng) phát sinh khi một ứng dụng nhận dữ liệu từ một nguồn không đáng tin cậy và đưa dữ liệu đó vào các phản hồi HTTP sau đó theo cách không an toàn.

Giả sử một trang web cho phép người dùng gửi bình luận về các bài đăng trên blog, được hiển thị cho những người dùng khác. Người dùng gửi bình luận bằng yêu cầu HTTP như sau:
```
POST /post/comment HTTP/1.1
Host: vulnerable-website.com
Content-Length: 100

postId=3&comment=This+post+was+extremely+helpful.&name=Carlos+Montoya&email=carlos%40normal-user.net
```
Sau khi bình luận này được gửi, bất kỳ người dùng nào truy cập bài đăng trên blog sẽ nhận được thông tin sau trong phản hồi của ứng dụng:  
`<p>This post was extremely helpful.</p>`  
Giả sử ứng dụng không thực hiện bất kỳ xử lý dữ liệu nào khác, kẻ tấn công có thể gửi bình luận độc hại như thế này:  
`<script>/* Bad stuff here... */</script>`  
Theo yêu cầu của kẻ tấn công, bình luận này sẽ được mã hóa URL thành:  
`comment=%3Cscript%3E%2F*%2BBad%2Bstuff%2Bhere...%2B*%2F%3C%2Fscript%3E`  
Bất kỳ người dùng nào truy cập bài đăng trên blog sẽ nhận được thông tin sau trong phản hồi của ứng dụng:  
`<p><script>/* Bad stuff here... */</script></p>`  
Sau đó, tập lệnh do kẻ tấn công cung cấp sẽ được thực thi trên trình duyệt của người dùng nạn nhân, trong bối cảnh phiên làm việc của họ với ứng dụng.  
> ### Tác động của Stored XSS
Nếu kẻ tấn công có thể kiểm soát một tập lệnh được thực thi trong trình duyệt của nạn nhân, thì thông thường chúng có thể xâm phạm hoàn toàn người dùng đó. Kẻ tấn công có thể thực hiện bất kỳ hành động nào có thể áp dụng cho tác động của lỗ hổng XSS được phản ánh .

Về khả năng khai thác, sự khác biệt chính giữa XSS phản chiếu và XSS lưu trữ là lỗ hổng XSS lưu trữ cho phép các cuộc tấn công tự chứa trong chính ứng dụng. Kẻ tấn công không cần phải tìm cách bên ngoài để dụ dỗ người dùng khác thực hiện một yêu cầu cụ thể có chứa khai thác của họ. Thay vào đó, kẻ tấn công đặt khai thác của họ vào chính ứng dụng và chỉ cần đợi người dùng gặp phải nó.

Bản chất khép kín của các khai thác tập lệnh chéo trang được lưu trữ đặc biệt có liên quan trong các tình huống mà lỗ hổng XSS chỉ ảnh hưởng đến những người dùng hiện đang đăng nhập vào ứng dụng. Nếu XSS được phản ánh, thì cuộc tấn công phải được tính thời gian một cách ngẫu nhiên: người dùng bị dụ thực hiện yêu cầu của kẻ tấn công vào thời điểm họ không đăng nhập sẽ không bị xâm phạm. Ngược lại, nếu XSS được lưu trữ, thì người dùng được đảm bảo đã đăng nhập vào thời điểm họ gặp phải khai thác.  
> ### Các bối cảnh khác nhau của Stored XSS
Có nhiều loại mã lệnh cross-site scripting được lưu trữ khác nhau. Vị trí của dữ liệu được lưu trữ trong phản hồi của ứng dụng xác định loại tải trọng nào cần thiết để khai thác nó và cũng có thể ảnh hưởng đến tác động của lỗ hổng.

Ngoài ra, nếu ứng dụng thực hiện bất kỳ xác thực hoặc xử lý nào khác trên dữ liệu trước khi dữ liệu được lưu trữ hoặc tại thời điểm dữ liệu được lưu trữ được đưa vào phản hồi, điều này thường sẽ ảnh hưởng đến loại tải trọng XSS cần thiết.  
> ### Cách tìm lỗ hổng Stored XSS
Nhiều lỗ hổng XSS được lưu trữ có thể được tìm thấy bằng trình quét lỗ hổng web của Burp Suite .

Kiểm tra các lỗ hổng XSS được lưu trữ theo cách thủ công có thể là một thách thức. Bạn cần kiểm tra tất cả các "điểm vào" có liên quan mà qua đó dữ liệu có thể kiểm soát được của kẻ tấn công có thể vào quá trình xử lý của ứng dụng và tất cả các "điểm thoát" mà dữ liệu đó có thể xuất hiện trong phản hồi của ứng dụng.

Các điểm nhập vào quá trình xử lý ứng dụng bao gồm:

Các tham số hoặc dữ liệu khác trong chuỗi truy vấn URL và nội dung tin nhắn.
Đường dẫn tệp URL.
Tiêu đề yêu cầu HTTP có thể không khai thác được liên quan đến XSS được phản ánh .
Bất kỳ tuyến đường ngoài băng tần nào mà kẻ tấn công có thể gửi dữ liệu vào ứng dụng. Các tuyến đường hiện có hoàn toàn phụ thuộc vào chức năng được ứng dụng triển khai: ứng dụng webmail sẽ xử lý dữ liệu nhận được trong email; ứng dụng hiển thị nguồn cấp dữ liệu Twitter có thể xử lý dữ liệu có trong các tweet của bên thứ ba; và trình tổng hợp tin tức sẽ bao gồm dữ liệu có nguồn gốc từ các trang web khác.
Điểm thoát cho các cuộc tấn công XSS được lưu trữ đều là các phản hồi HTTP có thể được trả về cho bất kỳ loại người dùng ứng dụng nào trong mọi tình huống.

Bước đầu tiên trong quá trình kiểm tra lỗ hổng XSS được lưu trữ là xác định các liên kết giữa điểm vào và điểm ra, theo đó dữ liệu được gửi đến điểm vào được phát ra từ điểm ra. Lý do tại sao điều này có thể khó khăn là:

Dữ liệu được gửi đến bất kỳ điểm nhập nào về nguyên tắc có thể được phát ra từ bất kỳ điểm thoát nào. Ví dụ, tên hiển thị do người dùng cung cấp có thể xuất hiện trong nhật ký kiểm tra tối nghĩa mà chỉ một số người dùng ứng dụng mới có thể nhìn thấy.
Dữ liệu hiện đang được ứng dụng lưu trữ thường dễ bị ghi đè do các hành động khác được thực hiện trong ứng dụng. Ví dụ, chức năng tìm kiếm có thể hiển thị danh sách các tìm kiếm gần đây, danh sách này sẽ nhanh chóng được thay thế khi người dùng thực hiện các tìm kiếm khác.
Để xác định toàn diện các liên kết giữa các điểm vào và ra sẽ bao gồm việc kiểm tra từng hoán vị riêng biệt, gửi một giá trị cụ thể vào điểm vào, điều hướng trực tiếp đến điểm ra và xác định xem giá trị có xuất hiện ở đó hay không. Tuy nhiên, cách tiếp cận này không thực tế trong một ứng dụng có nhiều hơn một vài trang.

Thay vào đó, một cách tiếp cận thực tế hơn là làm việc một cách có hệ thống thông qua các điểm nhập dữ liệu, gửi một giá trị cụ thể vào từng điểm và theo dõi phản hồi của ứng dụng để phát hiện các trường hợp giá trị đã gửi xuất hiện. Có thể đặc biệt chú ý đến các chức năng ứng dụng có liên quan, chẳng hạn như bình luận trên các bài đăng trên blog. Khi giá trị đã gửi được quan sát thấy trong phản hồi, bạn cần xác định xem dữ liệu có thực sự được lưu trữ trên các yêu cầu khác nhau hay không, trái ngược với việc chỉ được phản ánh trong phản hồi ngay lập tức.

Khi bạn đã xác định được các liên kết giữa các điểm vào và ra trong quá trình xử lý của ứng dụng, mỗi liên kết cần được kiểm tra cụ thể để phát hiện xem có lỗ hổng XSS được lưu trữ hay không. Điều này bao gồm việc xác định ngữ cảnh trong phản hồi nơi dữ liệu được lưu trữ xuất hiện và kiểm tra các tải trọng XSS ứng viên phù hợp có thể áp dụng cho ngữ cảnh đó. Tại thời điểm này, phương pháp kiểm tra về cơ bản giống như để tìm lỗ hổng XSS Reflected

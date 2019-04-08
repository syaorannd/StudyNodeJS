# Tổng quan
Node là một nền tảng phát triển các ứng dụng web back-end được viết bằng javascript, tức là Node không được viết để chạy trên trình duyệt, nếu bạn từng học Javascript thông thường thì bạn sẽ thấy Node chạy khác với những gì bạn đã học, bạn sẽ không thấy những thứ như document.getElementById()... mặc dù thực tế vẫn có một sôt thư viện hỗ trợ Node viết cho trình duyệt, tuy nhiên chúng ta sẽ không quan tâm đến chúng trong series này.

Ngoài việc chạy trên javaScript thì Node có những tính năng kèm theo:
- Có trình CLI( giao diện dòng lệnh)
- Chạy theo mô hình REPL
- Có các hàm quản lý tiến trình
- Có các đối tượng hỗ trợ làm việc với dữ liệu nhị phân
- Hỗ trợ TCp và UDP
- Hỗ trợ phân giải UDP
- Hỗ trợ HTTP và HTTPS
- Có thể truy cập file và thư mục

Node cho phép bạn thực hiện các giao thức mạng ở cấp độ thấp một cách dễ dàng. Chẳng hạn như Node có module HTTP cho phép xây dựng một webserver chỉ với vài dòng code, tuy nhiên vì thế mà bạn sẽ phải học nhiều thứ hơn như học về các header của một gói tin HTTP, không như PHP vốn chỉ là một module mở rộng của một webserver có sẵn ( như Apache hay Ngĩn...) - tức là PHP dễ dùng hơn Node nhưng lại không cho phép coder thực hiện các công việc ở cấp độ thấp. Tuy nhiên vì NodeJS là một framework mã nguồn mở, do đó trên mạng cũng có một số thư viện viết webserver nhanh hơn và dễ hơn cho coder.
# Kiến trúc của Node
Node sử dụng kiến trúc lập trình sự kiện không đồng bộ, và đây là một tính năng làm cho ứng dụng Node có thể chạy với hiệu xuất cao. Chẳng hạn như đối với các ứng dụng bình thường như một chương trình viết bằng C++ thì khi chúng ta viết chương trình để đọc dữ liệu, chương trình sẽ phải dừng lại ở đoạn code đọc dữ liệu để chờ cho đến khi có dữ liệu để đọc, nếu muốn chương trình tiếp tục vừa chạy các công việc khác vừa đọc dữ liệu thì phải dùng đến đa luồng ( multi-threading), tuy nhiên việc dùng đa luồng rất phức tạp và có thể làm chậm server.
Node chỉ sử dụng một luồng duy nhất, các câu lệnh nhập xuất không cần phải chờ bằng cách sử dụng **Event Loop**, cứ mỗi lần có sự kiện xảy ra thì chuyển dữ liệu của sự kiện đó đến các hàm sử lý tương ứng, và trong khi các hàm xử lý đang chạy thì vòng lặp sự kiện vẫn tiếp tục nhận sự kiện và chuyển đến các hàm xử lý tương ứng khác.
Ví dụ giả sử chúng ta có dòng code lấy dữ liệu từ cơ sở dữ liệu như sau:
```
result = query('SELECT * from db');
// xử lý result 
```
Đối với các chương trình bình thường thì khi chạy đến dòng code trên, luồng chạy chương trình đó sẽ phải dừng lại để đợi quá trình xử lý cơ sở dữ liệu thực hiện xong và trả về rồi mới tiếp tục được, trong quá trình đợi đó sẽ có nhiều yêu cầu khác xảy ra và hiệu xuất phần mềm giảm do lãng phí tài nguyên, để giải quyết tình trạng đó thì chúng ta có thể dùng cơ chế đa luồng để xử lý, tuy nhiên đa luồng có một nhược điểm là làm tiêu tốn nhiều bộ nhớ và CPU.
Thay vì dùng đa luồng thì Node sử dụng cơ chế Event Loop để giải quyết việc này, nó một cách đơn giản thì node sẽ đưa ra các câu lệnh chờ trên vào một luồng khác là Event Loop để xử lý riêng, trong khi luồng chính vẫn sẽ chạy các công việc riêng của nó, và khi nào luồng chính "rảnh" rồi thì luồng Event Loop sẽ chuyển các công việc đã thực hiện xong trở về lại luồng chính. Và chính vì Node chỉ sử dụng 2 luồng nên tài nguyên hệ thông sẽ không bị chiếm nhiều như khi dùng cơ chế đa luồng, ngoài ra việc code sử dụng Event Loop đơn giản hơn nhiều, ví dụ:
```
query('SELECT * from db', function(err, result) {
	if(err) throw err;
	// xử lý result
});
```
Trong đoạn code trên, kết quả trả về từ hàm query() thay vì được gán vào một biến thì sẽ được truyền vào một hàm khác là function(err, result){...}, và hàm nãy sẽ được truyền luồng Event Loop và chờ cho đến khi luồng chính "rảnh" thì mới được chuyển qua.
#Tên gọi
Tên chính thức là **Node.js**, tuy nhiên chúng ta sẽ gọi tắt là Node cho đơn giản.



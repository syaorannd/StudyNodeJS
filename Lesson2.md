# Chạy file mã nguồn Node

Bạn có thể mở terminal lên và gõ lệnh node --help để xem hướng dẫn sử dụng Node
```
thinhnn@thinhnn-Vostro-3670:~$ node --help
Usage: node [options] [ -e script | script.js | - ] [arguments]
       node inspect script.js [arguments]
...
```
Ngay dòng đầu tiên là cách để chạy một file node, chỉ đơn giản là ghi lệnh node <tên file> ra là được, nếu muốn có thể thêm một số tùy chọn (options) và tham số đi kèm (arguments).
Bạn có thể dùng bất cứ trình editor nào để viết code đều được. Dĩ nhiên là chúng ta nên dùng những editor có chức năng hiển thị code ( tức là có thể in màu những từ khóa như Notepad++... ) để làm việc cho dễ.
Ví dụ:
ls.js
```
var fs = require('fs');
var files = fs.readdirSyns('.');
for (fn in files) {
	console.log(files[fn]);
}
```
Chúng ta tạo một file có tên ls.js với đoạn code như trên.
Khi chạy file đó:
```
thinhnn@thinhnn-Vostro-3670:~$ node ls.js 
Desktop
Documents
Downloads
Music
NodeJS
Pictures
Public
PycharmProjects
Qt
Templates
Videos
VirtualBox VMs
app
appname
eclipse-java
eclipse-workspace
eclipse_JV
examples.desktop
flask
local
ls.js
node_modules
pycharm-2019.1.1
simsimi
snap
vmware
```
Đoạn code trên làm công việc liệt kê danh sách các file và thư mục hiện tại, tức là thư mục chưa file ls.js. Chúng ta sẽ tìm hiểu chi tiết chức năng của từng dòng code ở các bài sau. Bây giờ chúng ta sẽ tìm hiểu cách truyền tham số vào khi chạy. Đoạn code trên sửa lại như sau:
ls.js
```
var fs = require('fs');
var dir = '.';
if(process.argv[2])
	dir = process.argv[2];
var files = fs.readdirSync(dir);
for(fn in files) {
	console.log(files[fn]);
}
```
Khi chạy chúng ta có thể thêm tham số là đường dẫn một thư mục bất kỳ vào sau tên file. Ví dụ:
```
node ls.js Desktop/
54523515_2604900702860453_2742512879658860544_n.jpg
Java
Lập trình Web tốc độ cao, thời gian thực với NodeJS -
Music
NodeJS
Tron-bo-NodeJS-sieuthuthuat.com
eclipse
eclipse_C++
eclipse_server
fspeclipse
myapp
wearable
```
Khi chạy, đường dẫn Desktop sẽ được truyền vào một mảng toàn cục có tên là process.argv. mảng này luôn chứa ít nhát là 2 phần tử, phần tử đầu tiên là đường dẫn đến gile node.exe trong thư mục cài đặt Node, phàn tử thứ 2 là đường dẫn đến file sẽ được dịch để chạy, ở đây là file ls.js, các phần tử tiếp theo nếu có, ở đây là Desktop/
# Tạo web server
Vì Node được phát minh để làm web nên hầu hết chúng ta sẽ viết web server rất nhiều trong suôt series này. Ở đây chúng ta sẽ viết một đoạn code nhỏ để kiểm tra thử:
app.js
```
var http = require('http');
http.createServer(function (req, res) {
	res.writeHead(200, {'Content-Type' : 'text/plain'});
	res.end('Hello, World\r');
}).listen(8080, '127.0.0.1');
console.log('Server running at http://127.0.0.1:8080');
```
Chúng ta tạo một file có tên app.js và viết đoạn code trên vào, sau đó chay:
```
node app.js
Server running at http://127.0.0.1:8080
```
Đây chỉ là một đoạn code đơn giản, chúng ta sẽ tìm hiểu thêm sau. Sau khi đã chạy thì chúng ta có thể mở trình duyệt lên và trỏ đến 127.0.0.1:8080 hoặc localhost:8080 để xem chuỗi trả về của server.
![hello](https://github.com/syaorannd/StudyNodeJS/blob/master/hello.png)

Bạn cũng lưu ý là đoạn code trên sẽ chạy vô thời hạn cho đến khi chúng ta ngắt chương trình (Ctrl + C trong terminal) chứ không giống như các đoạn code trước là chạy xong thì kết thúc.

# Phần mềm quản lý gói - npm
Bản thân Node không có gì đặc sắc, chỉ là một trình biên dịch JavaScript với một vài thư viện nhập xuất bất đồng bộ. Lý do Node phát triển mạnh mẽ là vì nó là mã nguồn mở, đặc trưng của mã nguồn mở là cộng đồng hỗ trợ rất lớn, có rất nhiều coder ngoài viết thư viện hỗ trợ cho Node. Bản thân Node có một phần mềm quản lý các gói thư viện này đó là npm, chúng ta có thể tải các gói thư viện về và sử dụng chúng ngay một cách dễ dàng với npm.
Ở các phiên bản cũ thì chúng ta phải cài thêm npm riêng khi cài Node, còn đối vói các phiên bản mới thì khi nào chúng ta cài Node thì npm cũng đã được cài sẵn rồi.
Chúng ta sẽ thử cài gói hexy với npm, đây là một công cụ cho phép xem địa chỉ bộ nhớ của từng byte trong một file dưới dạng số hệ 16. Để cài một gói thì chúng ta chạy lệnh npm install [tùy chọn] <tên gói>:
```
npm install -g hexy
```


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


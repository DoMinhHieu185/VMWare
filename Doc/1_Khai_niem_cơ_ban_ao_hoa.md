# VMware Datacenter Virtualization Basics(Khái niệm cơ bản về ảo hóa trung tâm dữ liệu VMware)

### 1, Ảo hoá là gì?
* Là một môi trường ảo mô phỏng 1 máy vật lý
* Có các thành phần ảo tương tự như máy tính thật
  * CPU, Memory, Network Interface và Storage
* Nhiều máy ảo có thể cùng tồn tại trong một máy vật lý duy nhất.

<h3>Các thành phần Virtual Machine VMware</h3>

* Hệ điều hành(OS): Windows, MacOS, Linux
* VMware tools: là một bộ tiện ích giúp nâng cao hiệu suất của hệ điều hành khách của máy ảo và cải thiện việc quản lý máy ảo. Nó bao gồm trình điều khiển thiết bị và phần mềm khác cần thiết cho máy ảo
* Tài nguyên ảo:
  * CPU và memory
  * Network adapters
  * Disks và controllers

### 2, Máy ảo hoạt động như thế nào?
Máy ảo chạy như một tiến trình trong cửa sổ ứng dụng, tương tự như bất kỳ ứng dụng nào khác, trên hệ điều hành của máy vật lý. Các tệp chính tạo nên một máy ảo bao gồm tệp nhật ký, tệp cài đặt NVRAM, tệp đĩa ảo và tệp cấu hình. 

### 3, Lợi ích của việc sử dụng ảo hoá
* Sử dụng phần cứng tốt hơn 
* Giảm chi phí
* Không gian trung tâm dữ liệu
* Chi phí bảo trì định kỳ
* Tiết kiệm thiết bị mạng
* Sử dụng tốt storages

### 4, Những thách thức
* Chi phí cao cho những thiết bị chuyên dụng
* Một điểm lỗi duy nhất
* Tắc nghẽn hiệu suất: Tất cả không gian trên máy ảo đều có giới hạn

### 5, Các loại ảo hoá
#### 5.1, Desktop
tách môi trường máy tính để bàn khỏi thiết bị vật lý và lưu trữ máy tính để bàn trên một máy chủ từ xa, cho phép người dùng truy cập máy tính để bàn của họ từ mọi nơi trên mọi thiết bị.
* Máy ảo (VM) là một máy tính vật lý nhưng ở dạng phần mềm. Máy ảo được tổ chức bằng cách sử dụng hypervisors, giúp máy tính vật lý và máy ảo chạy như ý muốn.
* phép mọi người truy cập nhiều ứng dụng và hệ điều hành (HĐH) trên một máy tính duy nhất vì các ứng dụng và HĐH được cài đặt trên các máy ảo chạy trên một máy chủ trong trung tâm dữ liệu
* hai phương pháp chính
  * local: có nhiều hạn chế, bao gồm cả việc không thể sử dụng thiết bị di động để truy cập tài nguyên mạng
  * remote: phổ biến và người dùng chạy hệ điều hành và ứng dụng được truy cập từ máy chủ đặt bên trong trung tâm dữ liệu an toàn.

Đối với doanh nghiệp, ảo hoá Desktop cho phép nhân viên đăng nhập từ xa trong trường hợp thiên tai hoặc vấn đề về sức khoẻ khiến họ không thể đến văn phòng để làm việc

#### 5.2, Application
Tạo một phiên bản ảo của các ứng dụng cần thiết.
* Thông qua ảo hoá ứng dụng, người dùng có thể truy cập phiên bản từ xa của một ứng dụng chưa được cài đặt trên máy tính cá nhân
* Khi được ảo hoá, các ứng dụng hoạt động trong cái được gọi là sandbox, một môi trường chạy riêng biệt với hệ điều hành
* Khi hoạt động trong sandbox này, mọi thay đổi sẽ xuất hiện trong hệ điều hành, mặc dù ứng đụng đang lấy năng lượng hoạt động từ sandbox.
* Có 2 phương pháp ảo hoá aplication
  * remote: Chạy trên 1 máy chủ tương tự màn hình của người dùng và người dùng được uỷ quyền có thể truy cập mọi lúc, mọi nơi
  * Chỉ chạy 1 phiên bản trên máy chủ, cung cấp quền truy cập cục bộ vào ứng dụng

#### 5.3, Server
* Ảo hóa máy chủ cho phép phân chia tài nguyên tốt hơn, vì nó cho phép quản trị viên chia một máy chủ vật lý thành nhiều máy chủ ảo.
* các máy chủ ảo này có thể được sử dụng để chạy một hệ điều hành riêng biệt và bất kỳ ứng dụng nào cần thiết
* Máy chủ ảo chia sẻ CPU, Memory, storage và mạng được lấy từ hypervisor của máy chủ vật lý mà máy chủ ảo được xây dựng trên đó.

#### 5.4, Storages
Bộ nhớ có thể được ảo hóa bằng cách hợp nhất nhiều thiết bị lưu trữ vật lý để xuất hiện như một thiết bị lưu trữ duy nhất. Các lợi ích bao gồm tăng hiệu suất và tốc độ, cân bằng tải và giảm chi phí. Ảo hóa lưu trữ cũng giúp lập kế hoạch khôi phục sau thảm họa, vì dữ liệu lưu trữ ảo có thể được sao chép và nhanh chóng chuyển đến vị trí khác, giảm thời gian chết.  

#### 5.5, Network
Ảo hóa mạng là một tiến trình hợp nhất tài nguyên, thiết bị mạng cả phần cứng lẫn phần mềm thành một hệ thống mạng ảo. Sau đó, các tài nguyên này sẽ  được phân chia thành các channel và gắn với một máy chủ hoặc một thiết bị nào đó.
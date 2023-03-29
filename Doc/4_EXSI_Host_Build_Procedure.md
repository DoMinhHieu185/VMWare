# Quy trình xây dựng máy chủ EXSI

## Nội dung
* Các khái niệm cơ bản về ảo hoá
* Tổng quan về ESXi
* Quy trình Buid host ESXi
* Lab - Cài đặt ESXi
### 1. Các khải niệm ảo hoá cơ bản
Ảo hoá có nghĩa là nó là một công nghệ cho phép bạn chuyển đổi phần cứng thành phần mềm
**Host/Node/Server:**

![](F:\GITHUB\WMWare\img\14.png)

* máy chủ vật lý cung cấp tài nguyên cho ESXI hypervisor
* Ví dụ: Máy chủ vật lý HPE, DELL,IBM,fujitsu...

**Operating System:**

* Phần mềm được thiết kế để phân bổ tài nguyên vật lý cho các ứng dụng
* Ví dụ: MS Windows, Linux, Solaris.

**Hypervisor:**
* Hệ điều hành hoặc Phần mềm chuyên dụng để chạy máy ảo
* Ví dụ: ESXi, VMW Workstation, Fusion, MS Hyper-V & Oracle Virtual Box

**Virtual Machine:**
* Nó là một máy được tạo ra bằng phần mềm và trông giống như một máy chủ vật lý
* Ứng dụng chuyên dụng trừu tượng hoá tài nguyên phần cứng thành phần mềm.
* Ví dụ: ESXi - VMs, MS Hyper-V - VMs, Oracle Virtual Box VMs

**Guest OS:**

![](F:\GITHUB\WMWare\img\15.png)

* Hệ điều hành chạy trong Máy ảo
* Ví dụ: MS Windows, Linux, Solaris.

**Application:**
* Phần mềm chạy trên hệ điều hành, sử dụng tài nguyên vật lý hoặc ảo
* Ví dụ: MS Office, Chrome, SAP, MS SQL, Oracle,...

**vSphere:**
* Sản phẩm ảo hoá server của VMware kết hợp ESXi Hypervisor và vCenter Server Management Platform.

### 2. Tổng quan về ESXI

![](F:\GITHUB\WMWare\img\15.png)

* ESXi là bare metal VMware vSphere Hypervisor.
* ESXI cài đặt trực tiếp trên máy chủ vật lý cho phép truy cập trực tiếp vào tất cả các tài nguyên máy chủ(CPU, Mem, Disk or Storage, NIC)
* Cho phép các máy ảo chạy với hiệu suất gần như nguyên bản,không giống như hosted hypervisors
* ESXi có thể cài đặt trên hard disk, SAN LUNs, SD Card, SATADOM.
* ESXi có một small disk footprint để tăng cường bảo mật và độ tin cậy.
* ESXi 7.x cho phép
  * Sử dụng lên đến 768 Logical CPUs trên mỗi host
  * Sử dụng lên đến 16 TB RAM trên mỗi host
  * Triển khai (Deployment) lên đến 1024 virtual machines trên mỗi host

### 3. Kiến trúc ESXi
![](F:\GITHUB\WMWare\img\16.png)

* Bên dưới là Storage and Network: để cài đặt host ESXi ta cần storage và Network để truy cập host ESXi từ hệ thống khác.

* Bên trong OS ESXi, lõi chính của hệ điều hành ESXI là VMkernel

  * Để có thể truy cập vào VMkernel này, ta có thể truy cập bằng Local Support Console (được gọi là ESXi Shell - cho phép kết nối với core VMkernel)
* VMware Management Framework là một hệ thống quản lý Agentless (Sau khi cài đặt ESXi xong chỉ cần mở trình duyệt gõ địa chỉ IP host ESXi nó sẽ chạy trang chủ ESXi, có nghĩa là không có Agent để quản lý host ESXi đó)

* CLI Commands để cấu hình và hỗ trợ

  * Giả sử muốn cấu hình bất cứ thứ gì có thể thực hiện từ chế độ đồ hoạ hoặc sử dụng giao diện dòng lệnh CLI

* Muốn theo dõi server có Common Information Model (CIM), dịch vụ này chạy ở VMkernel Level

  * Đây cũng là Giám sát phần cứng không Agent. Để giám sát host ESXi, ta không cần phải cài đặt bất kỳ Agent nào. Có thể dựa trên địa chỉ IP hoặc giao thức snmp để giám sát ESXi

=> Thành phần core của ESXi là VMkernel, để truy cập vào hạt nhân VM, ta có thể sử dụng trình Shell và nó không cần Agent nào để duy trì host ESXi, ta có thể config và support host ESXi bằng CLI Commands. Mục đích của ESXi là nó cho phép tạo ra máy ảo và nó cũng yêu cầu storage và network để quản lý host ESXi.

### 4. ESXi Host Build Procedure
#### 4.1 Các bước trước khi cài đặt ESXi
- Xác minh danh sách tương thích phần cứng
- Chọn phần cứng tương thích (Máy chủ Tower/Rack mount/ Blade)
- Hệ thống cáp máy chủ hoạt động với sự trợ giúp của Nhà cung cấp
- Định cấu hình HPE-ILO hoặc DELL- IDRAC hoặc IBM- RSA hoặc Fujitsu - iRMC
- Kết nối với các Máy chủ bằng địa chỉ IP quản lý từ xa
- Cài đặt hoặc Upgrade Firmware mới nhất
- Bật RAID 1 hoặc 5 ở BIOS level
- Bật Intel-VT hoặc AMD-V ở BIOS Level
- Download tệp ESXi 7.x ISO hoặc tệp ISO Custom
- Nhận IP Settings từ Networking Team hoặc IP Inventory list (Danh sách kiểm kê IP)
- Nhận thông tin chi tiết về Storage từ Storage team.
- Tạo bản ghi host (A) và PTR records trong DNS server

#### 4.2 Quy trình cài đặt ESXi
- Mount ISO qua option Virtual media
- Reset Server vật lý bằng Power Mgmt.Option
- Theo dõi quá trình khởi động ESXi từ Remote Mgmt.Console
- Làm theo hướng dẫn trên màn hình để cài đặt, tức là nhấn F11

#### 4.3 Các bước sau khi cài đặt ESXi
- Thay đổi thông tin đăng nhập gốc qua SSH/Enable SSH
- Bật NTP, Port -123: Đồng bộ hoá theo thời gian (For Time Syncronization)
- Bật SNMP, Port - 161,162: Để giám sát máy chủ ESXi
- Áp dụng các bản vá lỗi trên host ESXi (Optional)
- Cấu hình Mạng host ESXi -vSwitch, DvSwitch
- Cấu hình Storage trên host ESXi - Local, NAS, ISCSI và SAN
- Chuyển nhương giấy phép ESXi (Assign ESXi License)
- Tắt chế độ ESXi lockdown
- Cấu hình ESXi Syslog server
- Xác thực trang thái kết nối host ESXi và kiểm tra Health
- Tạo một VMs Test và Kiểm tra image Backup
- Mở các port Firewall cần thiết (Optional)
- Xác thực Dung lượng disk host ESXi
- Set VMs auto start với host (Optional)

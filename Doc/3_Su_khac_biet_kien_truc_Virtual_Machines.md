# Sự khác biệt về kiến ​​trúc, Virtual Machines

### 1. Sự khác biệt về kiến trúc

Có 3 kiến trúc:
* Kiến trúc vật lý - **Traditional or Physical architecture**
* Kiến trúc dựa trên máy chủ - **Host based architecture**
* Kiến trúc kim loại trần - **Bare-metal architecture**

![](F:\GITHUB\WMWare\img\9.png)

#### 1.1. kiến trúc truyền thống hoặc vật lý
![](F:\GITHUB\WMWare\img\8.png)

* 64 Architecture, nó bao gồm các thành phần phần cứng chính là CPU, Memory và card mạng NIC, một bộ nhớ lưu trữ(ssd, flash drive)
* Trên phần cứng x64 Architectural đang cài đặt hệ điều hành (Operating System - OS), trên hệ điều hành là Applications (ms office, adobe,.. và bất kỳ ứng dụng bên thứ 3 nào khác)

#### 1.2. Kiến trúc dựa trên máy chủ
![](F:\GITHUB\WMWare\img\10.png)

* **x64 Architecture** là các phần cứng(CPU, RAM, DISK, network cark,....)
* Trên phần cứng sẽ cài hệ điều hành chủ (Operating System)
* Trên hệ điều hành chủ cài 1 phần mềm giám sát máy ảo (hay còn gọi là hypervisor). Các phần mềm phổ biến: VMware Workstation, VirtualBox, Hyper-V,...
* VMWare Workstation là một phần mềm ảo hoá cho phép tạo nhiều máy ảo cho mục đích thử nghiệm, trong hình có 3 máy ảo vm1,vm2.vm3
* Máy ảo cho phép cài dặt hệ điều hành khách và ứng dụng giống như một máy chủ vật lý
* Máy ảo cũng có các thành phần ảo, đây được coi là nhu cầu ảo vcpu, v-memory, vdisk và tương tự áp dụng cho các máy ảo cũng không chỉ 3 vms, dựa trên tài nguyên phần cứng, ta có thể tạo ra nhiều máy ảo trên 1 máy trạm vmware.

➟**Host based architecture** chỉ đượcc sử dụng cho các mục đích thử nghiệm, nó không phải cho mục đích sản xuất.

#### 1.3. Kiến trúc kim loại trần
![](F:\GITHUB\WMWare\img\11.png)

* Sự khác biệt của kiến trúc này so với kiến trúc dựa trên máy chủ là sẽ không cài hệ điều hành chủ mà sẽ cài phầm mềm ESXi trực tiếp trên phần cứng
* Trên máy chủ esxi nó cho phép bạn tạo nhiều máy ảo, trong sơ đồ này cho thấy có 3 vms: vm1 vm2 vm3.

➟Hầu hết môi trường sản xuất sử dụng kiến trúc kim loại trần

### 2. Các File Virtual Machine
Máy ảo – Virtual Machine : là 1 tập hợp gồm các file.

![](F:\GITHUB\WMWare\img\12.png)

Ta có thể chia làm 2 nhóm chính
  * Nhóm 1: Gồm những file khi tạo máy ảo ra là có (luôn có)
  * Nhóm 2: Khi sử dụng các tính năng thì mới xuất hiện.

Do khi tạo máy ảo, hệ thống phát sinh nhiều file nên sẽ chứa trong 1 thư mục có cùng tên với máy ảo và là tên duy nhất trên hệ thống.

* Nhóm 1: gồm các file
**<VM-Name>.vmx**: file chứa cấu hình máy ảo (ram, cpu, bao nhiêu card mạng, địa chỉ MAC ,vv.v). Đây là file quan trọng trong quá trình vận hành (quan trọng nhất).

**<VM-Name>.nvram**: chứa các cấu hình BIOS của máy ảo.

**Vmware.log**: file log, lưu thông tin, quá trình vận hành của máy ảo (edit cấu hình v.v.).

**<VM-Name>.vmdk**: file ổ cứng (cái này ta tự tao, nhưng cũng có thể coi như nhóm 1). Mỗi một ổ cứng, hệ thống tạo ra 2 file: <VM-Name>.vmdk và <VM-Name>-flat.vmdk. <VM-Name>-flat.vmdk lưu thông tin ổ cứng ảo (dung lượng, loại ổ cứng (thick hay thin…) v.v).

* Nhóm 2:
**<VM-Name>.vswp: swap file.**:

==> Khi một máy ảo tạo ra, hệ thống cấp tài nguyên vật lý cho máy ảo chạy. Như đã biết, ta có thể tạo lượng tổng  RAM của các máy ảo lớn hơn lương Ram vật lý ( 10 gb vẫn tạo được 4 máy 4GB). Nhưng những lúc các máy ảo hoạt động tối da, máy nào cũng cần 4GB thì làm sao đủ mà cung cấp ??. Lúc này , Vmware dự phòng bằng cách dùng Ram ảo (swap file) cho mỗi máy ảo. Dung lượng lớn nhất của swap file bằng với lượng Ram mà ta đã set cho máy ảo (swap file chỉ xuất hiện khi máy ảo power on + thiếu RAM).

**Suspend State file: <VM-Name>.vmss**:

Ta đã biết trên Windows, khi muốn tắt máy ta có 2  chế độ Shutdown  (close hết ứng dụng, giải phóng hết bộ nhớ). Hybernate( tắt máy , lưu trạng thái của Ram vào ổ cứng).

Thì trên Vmware cũng như vậy, Suspend cũng giống như Hybernate, Vmware lưu trạng thái của máy ảo trong **<VM-Name>.vmss**. File này co khi ta suspend máy ảo, dung lượng của nó bằng với dung lượng RAM.

**Snapshot file**:
lưu trạng thái máy ảo (lưu lại bộ file) ở từng thời điểm. Ta có thể restore lại máy ảo về đúng trạng thái đã snapshot.

Dùng để test các tính năng, phần mềm, bản vá lỗi

Bộ file gồm:
  * **Snapshot disk file (<VM_name>-delta.vmdk): vmdk** Chứa trạng thái của ổ cứng khi snapshop. Có nhiều file vmdk, mỗi vmdk sẽ đại diện cho từng thời điểm snapshot.
  * **Snapshot Data file(<VM_name>.vmsd)**: chứa danh sách những lần snapshot, lần snapshot nào thì dùng vmdk nào.
  * **Snapshot state file(<VM_name>.vmsn)**: File chứa trang thái RAM của máy ảo. Nếu ko co file này, chúng ta chỉ có thể revert trạng thái máy đã tắt. Nếu có những file này, máy ảo sẽ được khôi phục đúng nguyên trạng (ứng dụng, tiến trình đang chạy), hãy tưởng tượng giống như là hypernate vậy đó.

**Raw device map file(<VM_name>-rdm.vmdk)**: Thông thường, ổ cứng ảo là 1 file image. Chúng ta sẽ chứa dữ liệu trong virtual disk. Nếu ta muốn chứa trực tiếp trong  Lun (SAN)  thì dùng Raw Device Mapping File. Nó giúp LUN (SAN) kết nối trực tiếp đến máy ảo. RDM cũng có file mở rộng vmdk. Nhưng vmdk ở đây rất nhẹ (chỉ vài chuc kb).  Vmdk sẽ tiếp nhận lệnh đọc, ghi từ virtual machine để chuyển đến RDM ( nói là trực tiếp nhưng vẫn qua vmdk)

### 3. Chia sẻ tài nguyên vật lý

![](F:\GITHUB\WMWare\img\13.png)

* Có thể tạo VM trên:
  * VMware workstation
  * Hoặc máy chủ ESXi
* Ở bất kỳ máy ảo nào luôn tạo ra các vdisk, vmemory, vCPU. Tất cả đều được chia sẻ từ hệ thống vật lý
* Bất kể tài nguyên có sẵn trong máy tính vật lý có thể chia sẽ cho các máy ảo

### 4. Lợi ích của việc sử dụng Máy ảo
#### Máy vật lý
* Khó di dời
  * Các chuyển động yêu cầu thời gian chết. (Khi muốn di chuyển trung tâm dữ liệu từ nơi này sang nơi khác nếu là máy chủ vật lý phải thực hiện ngừng hoạt động cho máy chủ đó và có kế hoạch di chuyển máy chủ từ vị trí trì hoãn sang vị trí hoạt động, điều đó có nghĩa là rất khó để di đời )
* Khó quản lý:
  * Yêu cầu bảo dưỡng vật lý.
  * Lỗi phần cứng gây ra thời gian chết máy.
* Việc mở rộng, nâng cấp là phức tạp vì phải mua thiết bị phần cứng chuyên dụng

#### Máy ảo
* Dễ dàng di chuyển:
  * Đóng gói thành tệp (máy ảo có nghĩa nó trông giống như một phần mềm, nó trông giống như một máy chủ vật lý nhưng nó là một phần mềm được tạo ra bởi một lưới, nó bao gồm danh sách các tệp bạn chỉ cần sao chép tất cả vi tập tin bị lật và bạn có thể di chuyển tới bất cứ nơi nào bạn muốn, bạn có thể dễ dang di chuyển)
  * Độc lập với phần cứng vật lý
* Dễ dàng quản lý
  * Cách ly với các máy ảo khác
  * Cách ly với những thay đổi phần cứng.
* Hoàn toàn có thể nâng cấp và mở rộng tài nguyên khi cần thiết

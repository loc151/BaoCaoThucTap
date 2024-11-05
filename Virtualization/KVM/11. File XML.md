# Tìm hiểu file xml trong KVM

## File XML: 
- XML (eXtensible Markup Language) là một loại file có khả năng lưu trữ nhiều loại dữ liệu khác nhau. Mục đích của XML là đơn giản hóa việc chia sẻ dữ liệu giữa các hệ thống khác nhau, đặc biệt là các hệ thống được kết nối với internet.
- Một VM trong KVM có hai thành phần chính đó là VM's definition được lưu dưới dạng file XML và nằm trong thư mục `/etc/libvirt/qemu` và VM's storage lưu dưới dạng file image.
File domain XML chứa các thông tin về máy ảo như (số CPU, RAM, các thiết lập của I/O, card mạng,...)
- Ngoài file domain XML còn có các file XML khác để lưu thông tin network, storage...
Ta có thể thấy mỗi máy ảo được tạo ra có một file xml chứa các thông tin của nó.

![image](https://github.com/user-attachments/assets/5ab6a5fa-6238-4216-9eff-8f598704bac8)

- Sử dụng những lệnh sau để chỉnh sửa cấu hình VM trong file `.xml`:
```
virsh edit ubuntu22.04
hoặc
sudo nano /etc/libvirt/qemu/ubuntu22.04.xml
```

Trong file xml này chứa rất nhiều thông số nhưng ở đây chỉ đề cập đến một số thông số đáng chú ý:
![image](https://github.com/user-attachments/assets/39fcdd05-092f-4a9c-ab25-bb0371d9403a)

### Thẻ quan trọng không thể thiếu trong file domain xml là `domain`
- Tham số `type` cho biết hypervisor đang sử dụng của VM 
- Các tham số bên trong có ý nghĩa như sau:
	- `name`: Thông tin về VM
	- `uuid`: Mã nhận dạng quốc tế duy nhất cho máy ảo. Format theo RFC 4122. Nếu thiếu trường `uuid` khi khởi tạo, mã này sẽ được tự động generate
- Một số thẻ khác có thêm thông tin về các tham số như sau:
	- `title`: Tiêu đề của máy ảo
	- `description`: Đoạn mô tả của máy ảo
	- `metadata`: Chứa những thông tin về file xml
	- `memory`: Dung lượng RAM của máy ảo được cấp khi khởi tạo máy
	- `unit`: Đơn vị, mặc định là KiB
	- `currentMemory`: Dung lượng RAM đang được sử dụng tại thời điểm trích xuất file XML
	- `maxMemory`: Dung lượng RAM tối đa có thể sử dụng 
	- `vcpu`: Tổng số vcpu máy ảo được cấp khi khởi tạo

	- `vcpu` có một số tham số:
		- `cpuset`: Danh sách các cpu vật lý mà máy ảo sử dụng
		- `current`: Chỉ định cho phép kích hoạt nhiều hơn số CPU đang sử dụng 
		- `placement`: Vị trí của cpu, giá trị bao gồm static và dynamic 
	- Block OS: Chứa các thông tin về hệ điều hành của máy ảo
		- `arch`: Hệ điều hành thuộc kiến trúc 32 hay 64 bit 
		- `machine`: Thông tin về kernel của hệ điều hành
		- `loader`: Readonly có giá trị yes hoặc no chỉ ra file image writable hay readonly, type có giá trị rom hoặc pflash chỉ ra nơi guest memory được kết nối
		- `kernel`: Đường dẫn tới kernel image trên hệ điều hành máy chủ
		- `initrd`: Đường dẫn tới ramdisk image trên hệ điều hành máy chủ
		- `cmdline`: Xac định giao diện điều khiển thay thế
- Hành động xảy ra đối với một số sự kiện của OS 
	- `on_poweroff`: Hành động được thực hiện khi người dùng yêu cầu tắt máy
	- `on_reboot`: Hành động được thực hiện khi người dùng yêu cầu reset máy
	- `on_crash`: Hành động được thực hiện khi có sự cố
- Những hành động được phép thực thi:
	- `destroy`: Chấm dứt và giải phóng tài nguyên
	- `restart`: Chấm dứt rồi khởi động lại giữ nguyên cấu hình
	- `preserve`: Chấm dứt nhưng dữ liệu vẫn được lưu lại
	- `rename-restart`: Khởi động lại với tên mới
	- `destroy` và `restart` được hỗ trợ trong cả `on_poweroff` và `on_reboot`, `rename-restart` dùng trong `on_poweroff` 

- **CPU**: Khuyến cáo đối với CPU model, các tính năng và cấu trúc liên kết của nó có thể được xác định bằng cách sử dụng tập hợp các phần tử sau
	```sh
	...
	<cpu match='exact'>
	    <model fallback='allow'>core2duo</model>
	    <vendor>Intel</vendor>
	    <topology sockets='1' cores='2' threads='1'/>
	    <cache level='3' mode='emulate'/>
	    <feature policy='disable' name='lahf_lm'/>
	</cpu>
	...
	```
	```sh
	<cpu mode='host-model'>
	    <model fallback='forbid'/>
	    <topology sockets='1' cores='2' threads='1'/>
	</cpu>
	```
	```sh
	<cpu mode='host-passthrough'>
	    <cache mode='passthrough'/>
	    <feature policy='disable' name='lahf_lm'/>
	...
	```

- CPU chứa các mô tả yêu cầu của guest CPU, thuộc tính `match` của nó xác định mức độ liên kết của CPU ảo được cung cấp cho guest phù hợp với các yêu cầu này. Một số giá trị mà `match` có thể có là:
	- `minimum`
	- `exact`
	- `strict`
	- `clock`: Thiết lập về thời gian
		```sh
		<clock offset='utc'>
		    <timer name='rtc' tickpolicy='catchup'/>
		    <timer name='pit' tickpolicy='delay'/>
		    <timer name='hpet' present='no'/>
		</clock>
		```
	- `offset`: Giá trị utc, localtime, timezone, variable
	- `feature`: Là hypervisors cho phép thao tác một số tính năng như bật/tắt
		```sh
		<features>
		  <pae/>
		  <acpi/>
		  <apic/>
		  <hap/>
		  <privnet/>
		  <hyperv>
		    <relaxed state='on'/>
		    <vapic state='on'/>
		    <spinlocks state='on' retries='4096'/>
		    <vpindex state='on'/>
		    <runtime state='on'/>
		    <synic state='on'/>
		    <reset state='on'/>
		    <vendor_id state='on' value='KVM Hv'/>
		    <frequencies state='on'/>
		    <reenlightenment state='on'/>
		    <tlbflush state='on'/>
		  </hyperv>
		  <kvm>
		    <hidden state='on'/>
		  </kvm>
		  <pvspinlock state='on'/>
		  <gic version='2'/>
		  <ioapic driver='qemu'/>
		  <hpt resizing='required'>
		    <maxpagesize unit='MiB'>16</maxpagesize>
		  </hpt>
		  <vmcoreinfo state='on'/>
		  <smm state='on'>
		    <tseg unit='MiB'>48</tseg>
		  </smm>
		  <htm state='on'/>
		</features>
		```
		- `pae`: Chế độ địa chỉ vật lý mở rộng cho phép 32 bit và lớn hơn 4 GB RAM
		- `acpi`: Sử dụng trong việc quản lý máy ảo, ví dụ bắt buộc tắt máy
	- Ngoài ra còn các thẻ khác như: `apic`, `hap`, `viridian`, `privnet`, `hyperv`, `pvspinlock`, `kvm`, `pmu`, `vmport`, `gic`, `smm`, `ioapic`, `hpt`, `vmcoreinfo`, `htm`
	- Block device: Khai báo thông tin về thành phần của máy ảo như disk, network..
		- `emulator`: Khai báo đường dẫn tới thư viện ảo hóa các device
		- `device='disk'`: Khai báo thông tin về disk của máy ảo
		```sh
		<disk type='file' device='cdrom'>
		    <driver name='qemu' type='qcow2'/> : định dạng disk
		    <source file='/var/lib/libvirt/images/ubuntu22.04.qcow2'/>: Đường dẫn chứa disk
		    <target dev='vda' bus='virtio'/>: Tên ổ, kiểu ảo hóa
		    <boot order='2'/>: Thứ tự ưu tiên boot của ổ.
		    <address type='pci' domain='0x0000' bus='0x04' slot='0x00' function='0x0'/>
		</disk>
		```
		- `device='cdrom'`: Thông tin về ổ đĩa CDROM
		```sh
		<disk type='file' device='cdrom'>
		    <driver name='qemu' type='raw'/>
		    <target dev='sda' bus='sata'/>
		    <readonly/>
		    <boot order='1'/>
		    <address type='drive' controller='0' bus='0' target='0' unit='0'/>
		...
		</disk>
		```
	- Interface: Khai báo thông tin về Network
  ![image](https://github.com/user-attachments/assets/4422aed0-41d7-4288-b28d-72a8a9652498)


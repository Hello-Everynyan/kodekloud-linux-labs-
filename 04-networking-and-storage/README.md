Linux DNS: 7 questions
    1. Vào /etc/resolv.conf để xem địa chỉ IP của dns server dùng trong hệ thống
    2. File nào chịu trách nhiệm cho việc phân giải DNS dựa trên file host: /etc/hosts
    3. Tệp cấu hình nào được sử dụng cho máy chủ DNS: /etc/resolv.conf
    4. Đổi DNS Server thành Google's DNS (8.8.8.8): vi /etc/resolv.conf
    5. Tệp nsswitch.conf kiểm soát thứ tự mà hệ thống của bạn tra cứu tên máy chủ, xác định xem nó kiểm tra DNS hay tệp hosts trước.
        Chuyển sang quyền super-user và chạy lệnh grep hosts /etc/nsswitch.conf để kiểm tra thứ tự hiện tại 
         được sử dụng để giải quyết địa chỉ IP trong hệ thống
    6. Đổi thứ tự thành DNS rồi tới hosts
    7. domain search nào đang được cấu hình trong hệ thống
    
Question: Cái việc mà phân giải dns hay files trước có ảnh hưởng gì không?
Việc xác định thứ tự phân giải DNS hoặc file hosts ảnh hưởng đến cách hệ thống tìm kiếm địa chỉ IP 
 của tên miền. Nếu hệ thống kiểm tra /etc/hosts trước, nó sẽ ưu tiên dùng thông tin trong đó, 
  giúp giảm thời gian truy vấn DNS hoặc tránh lỗi nếu DNS gặp sự cố.

Ví dụ: Giả sử bạn có một mục trong /etc/hosts như sau:
192.168.1.100   myserver.local

Nếu hệ thống kiểm tra /etc/hosts trước DNS, khi bạn truy cập myserver.local, 
 nó sẽ dùng địa chỉ IP 192.168.1.100 ngay lập tức mà không cần hỏi DNS. 
  Nếu thứ tự ngược lại, hệ thống sẽ gửi yêu cầu đến DNS trước, 
   có thể mất thêm thời gian hoặc không tìm thấy nếu DNS không có thông tin.


Linux Networking: 13 questions
  1. Câu đầu hỏi địa chỉ IP nào đang được gán trên giao diện mạng chính: dùng ip a
  2. Hỏi tên của giao diện có IP được gán | ví dụ: "eth0@if94428:" thì là etho0
  3. Hỏi defaulte gateway được cấu hình trong hệ thống: ip r
  4. Kiểm tra giao diện eth0 trên caleston-lp10, hỏi là nó có up không | ví dụ eth0@if94428: <BROADCAST,MULTICAST,UP,LOWER_UP>
  5. Lệnh nào được dùng để liệt kê và chỉnh sửa network interfaces trên 1 Linux host: ip link
  -> ip link set dev <ten_giao_dien> up (or down)
  -> ip link set dev <ten_cu> name <ten_moi>
  6. Lệnh nào dùng để xem địa chỉ IP được gán vào network interfaces on a Linux host: ip addr
  7. Nhiệm vụ chính của router trong mạng: kết nối 2 hay nhiều mạng
  8. 0.0.0.0 trong gateway của bảng định tuyến nghĩa là gì:
  9. Lệnh nào dùng để thêm 1 entry mới vào kernel routing table: ip route add
  10. Khi mà thay đổi dịa chỉ ip với ip addr add, nó sẽ bị mất nếu máy restart, vậy phải lưu ở đâu: /etc/network/interfaces
  11. Giới hạn của switch trong mạng: chỉ vận chuyển được các gói tin trong cùng 1 mạng
  12. How many network interfaces (including loopback) are currently listed on caleston-lp10?: ip link and count (2)
  13. According to the lecture, which keyword can be used in place of 0.0.0.0
  when specifying a catch-all destination in a routing table entry? default

Linux Storage 2: 6 questions
    1 - Cách biết có bao nhiêu disk dạng block devices trong system -> lsblk
    2 - size của disk /dev/vdd
    3 - major number của thiết bị begin với vd, số major đây là số mấy: 252
    4 - max partitions mà MBR có thể có là 4
    Giải thích: Hãy nghĩ về MBR như một chiếc hộp đựng tối đa 4 phần riêng biệt. Đó là giới hạn của nó, gồm cả phân vùng chính và mở rộng.
    5 - Bao nhiêu partitions mà disk /dev/vda có hiện tại: 3 (không tính vda)
    Có thể thấy khi lsblk:
    vda
        -vda1
        -vda14
        -vda15 
Quan trọng 6 - Tạo một partition GPT tên vde1 với kích thước 500M trên ổ /dev/vde
    sudo gdisk /dev/vde | chạy lệnh để mở công cụ gdisk trên đĩa /dev/vde
    khi hỏi command (? for help) thì bấm n để tạo phân vùng mới
    select partition number = 1 (vì mình chỉ tạo 1 phân vùng)
    select default first sector = 2048 (mặc định là 2048) (nếu tạo các vùng tiếp theo thì là 2049 2050,...)
    select +500M when asked for last sector (chọn kích thước cho phân vùng)
    use default hex code (mã hex mặc định 8300, đại diện cho phân vùng Linux) (mã hex cho windows là 0700, đại diện cho phân vùng NTFS hoặc FAT32)
    hỏi command (? for help): thì ghi w (để ghi các thay đổi vào bảng phân vùng)
    khi ok rồi thì nó sẽ hiện "Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING PARTITIONS!!"
    Lưu ý: Hãy đảm bảo bạn đã chọn đúng đĩa và không cần giữ dữ liệu cũ, vì quá trình này sẽ xóa tất cả phân vùng hiện tại trên đĩa đó!

Linux Storage Filesystems: 7 questions
    1 - always use sudo
    2 - filesystems nào không dùng journal - ext2
    3 - hệ thống tập tin đã được tạo trên các đĩa /dev/vdd hoặc /dev/vde, hỏi là ổ đĩa nào đã có hệ thống tập tin được tạo -> dùng sudo blkid /dev/vde và sudo blkid /dev/vdd
    !!! blkid là lệnh để hiển thị thông tin về các thiết bị lưu trữ block, như:
        + phân vùng đĩa cứng, USB, v.v. Nó cho biết UUID, loại hệ thống tập tin (như ext2, ext3, ntfs) và các thuộc tính khác
        ví dụ khi chạy blkid thì nó sẽ hiện: /dev/vdd: UUID='dfags' BLOCK_SIZE="4096" TYPE="ext2"
    4 - hỏi là /dev/vdd type nào - ext2
    5 - Tạo filesystem ext4 trên disk /dev/vde và mount nó tại /mnt/data (mkfs là make filesystem)
    Bước đầu: sudo mkfs.ext4 /dev/vde
    Bước hai: sudo mkdir /mnt/data
    Bước ba: sudo mount /dev/vde /mnt/data
    6 - điều gì xảy ra với mount /mnt/data sau khi system reboot
    -> The mount is not persistent in FSTAB yet. If the system is rebooted, the filesystem will not be mounted
    7 - Làm cho mount lưu vĩnh viễn
    Bước 1: vào /etc/fstab
    Bước 2: thêm dòng /dev/vde /mnt/data ext4 rw 0 0
    Cú pháp của fstab:   <device> <mount_point> <filesystem_type> <options> <dump> <pass>
    Trong đó: 
        + <dump>: dùng để sao lưu, thường để 0 hoặc 1
        + <pass>: thứ tự để kiểm tra hệ thống tập tin khi khởi động, 0 nghĩa là không kiểm tra
        + rw là viết tắt của read-write
        + số đầu tiên là để hệ thống biết có cần sao lưu phân vùng này không (0 là không)
        + số thứ hai là để xác định thứ tự kiểm tra hệ thống tập tin khi khởi động (0 nghĩa là bỏ qua)
        

Linux Account Management: 11 questions
  1 - Always use sudo
  2 - Hỏi hiện tại bob là user gì trong system: user account
  3 - Lệnh nào sẽ show UID của 1 user: id (uid=... gid=... groups=...)
  4 - Hỏi UID của bob
  5 - Quyền sudo của bob làm được gì: install, reboot, remove
  6 - Nơi chứa mật khẩu đã được mã hóa: /etc/shadow
  7 - Một user mới tên chris đã được tạo, muốn biết full name: vào passwd xem
  8 - Chris thuộc group nào: id chris
  9 - Nhóm chính của chris: 
  10 - tạo 1 user mới và đặt mk: sudo useradd [ten] & sudo passwd [ten]
  11 - Tạo group tên john với gid là 1010. Tạo user khác tên john với uid = 1010
  group chính là john và login shell = /bin/sh
  -> sudo groupadd -g 1010
  -> sudo useradd -u 1010 -g 1010 -s /bin/sh john

Linux Permissions & Ownership: 9 questions
  1 - Always use sudo
  2 - 1 File mới được tạo và hỏi quyền owner của file đó: ls -l
  3 - Hỏi quyền group của file đó
  4 - Hỏi other
  5 - Hỏi owner của thư mực
  6 - File soccer được tạo dưới thư mục sports, có full quyền, yêu cầu đổi group và other thành r và execute -> chmod 755
  7 - Thêm write và xóa tất cả các quyền của other
  8 - Đổi ownership của file -> sudo chown [ten_nguoi_moi] [file]
  9 - Đổi toàn quyền từ thư mục cha đến con: chown -R

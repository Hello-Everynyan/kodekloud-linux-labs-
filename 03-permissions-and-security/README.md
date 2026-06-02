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

Linux SSH & SCP: 8 questions
  1 - port ssh: 22
  2 - nếu ssh devapp01 thì user tên là gì: bob
  3 - chuẩn bị tạo kết nối không cần pass tới server (password-less)
  4 - ssh-keygen -t rsa (nhớ đọc option của ssh-keygen)
  5 - public key tạo được lưu ở đâu: /home/bob/.ssh/id_rsa.pub (thường có extension là pub)
  6 - ssh-copy-id vào bob@devapp01 để gửi public key vào, thường phải nhập mk của bob@devapp01
  7 - file đưa vào server nằm ở đâu: /home/bob/.ssh/authorized_keys
  8 - dùng scp để copy file từ máy bob sang server -> scp /home/bob/caleston-code.tar.gz devapp01:/home/bob

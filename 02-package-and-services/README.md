Linux cronjobs: 7 questions
  1 - lệnh nào dùng để liệt kê tất cả các cronjobs được tạo cho 1 user
  -> crontab -l
  2 - có bao nhiêu cronjobs được lên lịch hiện tại cho bob
  -> crontab -l -> count: 6
  3 - có bao nhiêu cronjobs được lên lịch cho user root
  -> sudo crontab -l
  4 - Kiểm tra lịch trình của bob lần nữa, command/script nào được chạy lúc 11h tối kém 11 mỗi thứ 3
  -> 23 11 * * 2
Quan trọng: Được xếp theo: phút |giờ |ngày trong tháng |tháng |ngày trong tuần
  Thứ 3 là ngày THỨ hai trong tuần = 2
  5 - Tạo 1 lịch trình để chạy script cho ngày đầu tiên của mỗi tháng vào 6am
  -> 0 6 1 * * /usr/...
  6 - Khi nào script /usr/local/bin/system-troubleshooter.sh được chạy (của bob)
  7 - chỉnh script chạy mỗi 30 phút 
  -> */30 * * * *

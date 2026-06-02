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
 Lưu ý: muốn chỉnh lịch trình thì crontab -e

Linux systemd Services: 11 questions
  1 - Always use sudo
  2 - hỏi status của sample.service: sudo systemctl status sample.service
  3 - hỏi là start đc sample.service không -> không 
  4 - lí do start service fail -> dùng sudo journalctl -u sample.service
  5 - update service section = set the execStart to run the script /bin/bash /root/sample_script.sh
  start service khi xong
  -> sudo vi /etc/systemd/system/sample.service -> sau đó thêm /bin/bash /root/sample_script.sh vào dòng ExecStart -> sau khi xong thì restart service
  6 - Kiểm tra status của service 
  7 - enable service -> sudo systemctl enable sample.service
  8 - update service sao cho mỗi khi nó dừng thì luôn restart
  -> sudo vi /etc/systemd/system/sample.service -> add 'Restart=always' vào Service section
  9 - Yêu cầu restart service, sau đó hỏi là warning gì -> warning run 'systemctl daemon-reload' to reload units
  10 - chạy lệnh reload trên
  11 - hỏi là làm sao để check lỗi khi có biến -> sudo journalctl -u sample.service

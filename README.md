# Cấu hình IP tĩnh bằng NETPLAN
* Cấu hình mạng Netplan lần đầu tiên được giới thiệu bắt đầu từ Ubuntu 18.04, do đó Netplan có sẵn cho tất cả Ubuntu mới từ phiên bản này trở lên. Hãy bắt đầu với một số hiểu cơ bản về cách netplan hoạt động trên Ubuntu.
* Netplan cho phép cấu hình mạng thông qua cả hai: networkd daemon hoặc NetworkManager. networkd daemon chủ yếu được sử dụng cho cấu hình máy chủ, trong khi NetworkManager được sử dụng bởi người dùng GUI. Để chuyển đổi giữa cả hai, bạn cần chỉ định trình kết xuất một cách rõ ràng thông qua tệp cấu hình netplan.
* Vị trí tệp cấu hình netplan được đặt thành thư mục /etc/netplan/. Các vị trí có thể khác là /bib/netplan/ và /run/netplan/. Tùy thuộc vào cài đặt Ubuntu của bạn, tệp cấu hình Netplan thực tế có thể có một trong ba dạng sau:
    * 00-installer-config.yaml
* Để định cấu hình địa chỉ IP tĩnh trên máy chủ Ubuntu, bạn cần tìm và sửa đổi tệp cấu hình mạng netplan có liên quan. Xem phần trên để biết tất cả các vị trí và biểu mẫu tệp cấu hình Netplan có thể có. Ví dụ: bạn có thể tìm thấy tệp cấu hình netplan mặc định được gọi là 01-netcfg.yaml với nội dung sau hướng dẫn người dùng hỗ trợ mạng cấu hình giao diện mạng của bạn qua DHCP:
```

network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: yes
  ```
* Để đặt giao diện mạng của bạn `ens33` thành địa chỉ IP tĩnh `103.107.181.45` với cổng `103.107.181.1` và máy chủ DNS là `8.8.8.8` và `103.107.181.1`, và domain là`toilamlab.com` hãy thay thế cấu hình trên bằng cấu hình bên dưới.
![image](https://user-images.githubusercontent.com/91528234/197923650-ecde6c0e-800c-4c8a-bc34-ede50430abd5.png)
* Sau khi sẵn sàng, hãy áp dụng các thay đổi cấu hình Netplan mới bằng các lệnh sau:
```
# netplan apply
```
* Trong trường hợp bạn gặp phải một số vấn đề, hãy thực hiện:
```
netplan --debug apply
```
# Kiểm trả domain xem đã trỏ vào domain chưa
* Cấu hình 2 máy trong file `/etc/hosts` như sau:
```
vim /etc/hosts
```
* Máy chủ DNS server

![image](https://user-images.githubusercontent.com/91528234/197924590-007c3668-3ae4-4ef0-a1b2-681ea1387d66.png)
* Client
 
![image](https://user-images.githubusercontent.com/91528234/197924792-d1fc7f00-ebfa-4789-9f63-4a79212f5300.png)
* Kiểm trả domain xem đã trả về đúng giá trị IP tĩnh của DNS server chưa bằng lệnh `dig`
```
dig [domain_name]
```
![image](https://user-images.githubusercontent.com/91528234/197925072-5fecbe23-59c9-46b3-b379-3bced4fe012a.png)
* All done :heartpulse:

# Tầng mạng

**Nhắc lại kiến thức cơ bản về tầng mạng**
- Chức năng chung là điều khiển truyền dữ liệu giữa các nút mạng qua môi trường liên mạng, cụ thể hơn là:
    - Định tuyến(routing): xác định tuyến đường đi cho các gói tin từ đích đến nguồn
    - Chuyển tiếp(forwarding): chuyển các gói tin từ đầu vào tới đầu ra phù hợp của router
- Các protocol phổ biến ở tầng này: IP (Internet Protocol), ICMP (Internet Control Message Protocol

## IP - Internet Protocol

Là giao thức cơ sở của tầng mạng, là giao thức được định tuyến (routed protocol) tức đòi hỏi phải có các giao thức định tuyến để xác định trước đường đi cho dữ liệu. Ngoài ra còn là một giao thức connection-less (hướng không liên kết), các gói tin được xử lý độc lập, nhanh và không tin cậy (best-effort). IP hoạt động độc lập với môi trường truyền dẫn

Các chức năng cơ bản của IP:
- Định địa chỉ: địa chỉ IP
- Đóng gói dữ liệu: dồn kênh, phân kênh
- Chuyển tiếp: theo địa chỉ IP (sẽ đề cập sau)
- Quản lý đảm bảo chất lượng dịch vụ

### Địa chỉ IPv4

IPv4 header 20 - 60 bytes

Là một số 32 bit để định danh cổng giao tiếp mạng trên nút đầu cuối của bộ định tuyến router. Là một thứ có tính duy nhất (unique)

Có 2 cách để cấp phát địa chỉ IP, Static IP hay cấp phát cố định và cấp phát tự động thông qua DHCP (Dynamic Host Configuration Control)

Địa chỉ IP có 2 phần, Host ID hay địa chỉ máy trạm và Network ID hay địa chỉ mạng. Để biết được phần nào là Host ID phần nào là Network ID thì ta có 2 cách:
- Phân lớp địa chỉ: Chia cứng (fixed) IP thành các lớp A B C D E. Việc này có nhược điểm là lãng phí không gian địa chỉ
- => Ta có thằng vip hơn là CIDR (Classless Inter Domain Routing)

Về CIDR hay Classless Inter Domain Routing sẽ liên quan tới mặt nạ mạng (subnet mask hay netmask). Subnet mask sẽ chia một địa chỉ IP thành 2 phần:
- Phần ứng với máy trạm, máy chủ hay host
- Phần ứng với mạng

Mục đích của subnet mask là xác định xem 1 địa chỉ IP thuộc về mạng con nào, từ đó router hoặc máy tính có thể biết được phải xử lý gói tin như nào

### Địa chỉ IPv6
Header cố định 40 bytes

### DHCP - Dynamic Host Configuration Protocol

Sử dụng port 67 (host) 68 (client)

**Hoạt động chủ yếu ở tầng ứng dụng (transport UDP)**

Quy trình DORA (discover - Offer - Request - ACK)






### Phân loại class A B C D E:
- class A: Bit đầu bằng 0 với 7 bit network + 24 bit host
- class B: 1 0 với 14 bit network + 16 bit host
- class C: 1 1 0 với 21 bit network + 8 bit host
- class D: 1 1 1 0
- class E: 1 1 1 1

![image](https://github.com/user-attachments/assets/629e593a-0fef-495c-a066-bd909db4738f)


### Subnet (mạng con)
Hai máy tính được coi là nằm trong cùng 1 mạng con và có thể liên thông trực tiếp với nhau mà không cần qua thiết bị định tuyến trung gian nếu phần mạng (NetworkIDs) của địa chỉ IP giống hệt nhau

Để xác định phần mạng, ta thực hiện phép logic AND giữa IP và subnet mask. Ví dụ một câu hỏi như sau:

```
Trong mạng máy tính dùng giao thức TCP/IP và đều dùng Subnet Mask là
255.255.255.0 thì cặp máy tính nào sau đây liên thông:
A. 192.168.1.3 và 192.168.100.1
B. 192.168.15.1 và 192.168.15.254
C. 192.168.100.15 và 192.186.100.16
D. 172.25.11.1 và 172.26.11.2
```

> Giải: Ta có subnet mask là 255.255.255.0 tương đương với `11111111.11111111.11111111.00000000` => 24 bit đầu là phần network, 8 bit sau là phần host 
> Ta lấy các IP ở kết quả đổi sang binary và AND từng cặp để xem cái nào ra giống subnet mask thì chọn

Ví dụ về một câu hỏi khác yêu cầu tính số mạng con và số máy trong mỗi mạng con đó:
Công thức chung: số mạng con = 2 ^ (số bit mượn) - 2 và số máy = 2 ^ (số bit host) - 2


```
Địa chỉ mạng NetID: 192.168.0.32/27 có dãy địa chỉ máy HostIDs sử dụng tương
ứng là:
A
192.168.0.33 => 192.168.0.63
B
192.168.0.32 => 192.168.0.64
C
192.168.0.32 => 192.168.0.62
D
192.168.0.33 => 192.168.0.62
```

Đề yêu cầu tính HostIDS tức yêu cầu tính địa chỉ network và địa chỉ quảng bá. HostIDS sẽ nằm trong khoảng network + 1 và quảng bá - 1

Tính network và quảng bá thì đơn giản rồi, xét subnet mask để xem lấy bao nhiêu bit rồi chuyển phần host về toàn 0 và 1 => Bài này hiện ta có 32 là octet cuối cùng tương ứng 0010 0000 => Network là giữ nguyên tức 0010 0000 - 32còn broadcast là 0011 1111 tức 63 => khoảng là 33 đến 62


## Router

2 chức năng chính của router:
- Định tuyến: Xử lý giải thuật định tuyến
- Chuyển tiếp gói tin datagram từ liên kết vào tới liên kết ra
- Gateway Router: 

RIP sử dụng distance vector routing
OSPF xài link state

![image](https://github.com/user-attachments/assets/297db89b-3643-4c3c-9da8-22c955d7f3b9)


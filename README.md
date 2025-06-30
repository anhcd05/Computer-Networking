# Introduction to Computer Network
> * Ok trong modules này, ta sẽ được tìm hiểu về các công nghệ được sử dụng đằng sau các mô hình mạng máy tính (hay còn được biết tới với tên gọi: `Networking` hoặc `Networks`)
> * Chúng ta sẽ tập trung chủ yếu vào 2 loại hình chính: `Local Area Networks (LANs)` và `Wide Area Networks (WANs)`

## What is a Network?

Một mô hình mạng (network) là một tập hợp các thiết bị được kết nối với nhau, chúng có thể giao tiếp gửi - nhận dữ liệu cũng như chia sẻ tài nguyên với nhau.

Các thiết bị đầu cuối riêng lẻ này thường được gọi là `nodes`, có thể bao gồm máy tính, điện thoại, máy in và máy chủ. Tuy nhiên chỉ có mỗi nodes thì chưa thể hình thành được hoàn toàn một mô hình mạng máy tính.

![image](https://github.com/user-attachments/assets/b4015c13-9e27-4156-adf7-94ab0f491568)

Những ý trên nghe còn có vẻ hơi khó hiểu, nhưng nhìn chung thì ta có thể mô tả một mô hình mạng trong thực tế như sau:
* Giả sử có bạn cần gửi thư (online hoặc offline) tới một người bạn ở xa =>
    * Mỗi người sẽ sử dụng một thiết bị, đại diện cho 1 nodes
    * Links: có thể là hệ thống bưu điện (người gửi => xe tải trung chuyển => người nhận) hoặc hệ thống Internet
    * Data sharing: Nội dung bức thư

## Why are Networks important?
> I think it's easy tbh

## Types of Networks



|                    | Local Area Network | Wide Area Network |
| ----------- | -------- | -------- |
| Định nghĩa    | Một mạng LAN kết nối các thiết bị trong một khu vực nhỏ như trong nhà, trong khu vực trường học,...     | Một mạng WAN trải dài qua các khu vực và kết nối các mạng LANs lại với nhau    |
| Phạm vi | Chỉ một khu vực nhỏ | Có thể trải dài cả thành phố, đất nước, châu lục |
| Quyền sở hữu | Thường được sở hữu và quản lý bởi một cá nhân hoặc một tổ chức | Thường được sở hữu và quản lý bởi nhiều tổ chức, tập đoàn hoặc các nhà cung cấp dịch vụ mạng (ISP) |
| Tốc độ | Tốc độ truyền tải thông tin nhanh | Chậm hơn LANs vì quãng đường dài hơn và nhiều thiết bị trung gian |
| Phương thức kết nối | Sử dụng kết nối có dây (Ethernet cables) hoặc không dây như Wi-Fi | Sử dụng sợi quang, liên kết vệ tinh và các đường dây viễn thông |

## How do LANs and WANs work together?

![image](https://github.com/user-attachments/assets/5a035755-561f-4a7f-8725-03287c0adfdf)

Để giải thích cách mà các mạng LAN - WAN hoạt động chung với nhau, ta có thể mô tả nhỏ hơn như này:
* When accessing the Internet, a home LAN connects to an Internet Service Provider's (ISP's) WAN, which grants Internet access to all devices within the home network
> An ISP is a company that provides individuals and organizations with access to the Internet. In this setup, a device called a modem (modulator-demodulator) plays a crucial role
* The modem acts as a bridge between your home network and the ISP's infrastructure, converting digital signals from your router into a format suitable for transmission over various media like telephone lines, cable systems, and fiber optics
* This connection transforms a simple local network into a gateway to the resources available online.

# Application Layer - Tầng ứng dụng

**Nhắc lại các đặc điểm chính về tầng ứng dụng:**
- Là tầng cao nhất trong mô hình OSI và TCP/IP với đơn vị dữ liệu là data hoặc message
- Chức năng chính là cung cấp phương tiện để người dùng có thể truy nhập vào môi trường mạng, xác định giao diện **(keyword: interface)** giữa người dùng và môi trường
- Các giao thức, các vấn đề cần lưu ý ở tầng ứng dụng bao gồm:
    - HTTP
    - FTP
    - SMTP
    - SNMP
    - DNS
    - DHCP
    - Telnet

## Một số kiến trúc của ứng dụng

### Kiến trúc Client - Server
- Server:
    - Là host luôn hoạt động
    - Có địa chỉ IP cố định
- Client:
    - Có thể được kết nối liên tục vào mạng hoặc không
    - Có thể có địa chỉ IP thay đổi
    - Không truyền thông trực tiếp với Client khác

### Kiến trúc Peer-to-peer
- Không có Server luôn hoạt động
- Các hệ thống đầu cuối (gọi là peer) truyền thông trực tiếp với nhau
- Mỗi peer sẽ yêu cầu dịch vụ từ một peer nào đó và lại cung cấp dịch vụ này cho các peer khác => Có khả năng tự mở rộng
- Các peer không kết nối liên tục và có thể thay đổi địa chỉ IP => Quản lý phức tạp

### Mô hình lai
- Một Server trung tâm để quản lý Client và các thông tin khác
- Các máy Client sẽ liên lạc trực tiếp với nhau sau khi đăng nhập

## Định danh
Để nhận diện các thông điệp khác nhau, mỗi tiến trình cần phải có định danh (identifier). Định danh bao gồm cả địa chỉ IP và số hiệu cổng (port). Một số các range về port cũng như ý nghĩa được phân chia như sau:
- Từ 0 => 1023 (Well-known Ports): HTTP - 80, HTTPS - 443, FTP - 20 và 21, SSH 22, Telnet 23, SMTP 25, POP3 110, IMAP 143, DNS 53, DHCP 67 và 68, SNMP 161 và 162 ...
- Từ 1024 => 49151 (Registered Ports): MSSQL - 1433, MySQL - 3306, PostgreSQL - 5432, Oracle - 1521, Redis - 6379, MongoDB - 27017, OpenVPN - 1194 ...
- Từ 49152 => 65535 (Dynamic/Private Ports)

## HTTP - HyperText Transfer Protocol

HTTP sử dụng TCP, là giao thức "không trạng thái" tức Server không lưu giữ thông tin về những yêu cầu trước đó của user. HTTP có 2 loại kết nối chính, đó là:
- HTTP không bền vững (HTTP 1.0): 
    - Mở kết nối TCP
    - Chỉ có đúng một đối tượng được gửi qua một kết nối TCP 
    - Kết nối TCP được đóng lại
    - => Việc tải về nhiều đối tượng sẽ yêu cầu nhiều kết nối, tốn tài nguyên và đỗ trễ lớn. Thời gian đáp ứng của HTTP không bền vững = 2 RTT + thời gian truyền tệp

- HTTP bền vững (HTTP 1.1 và HTTP 2):
    - Mở kết nối TCP
    - Nhiều đối tượng có thể được gửi qua một kết nối TCP duy nhất
    - Kết nối TCP được đóng lại

Khái niệm mới: RTT (Round Trip Time) là thời gian để một gói tin nhỏ đi từ Client => Server rồi quay lại

- Về request và response: cơ bản quá lười ghi

Ngoài ra, HTTP là một stateless protocol tức các request sẽ được xử lý độc lập mà không liên quan gì đến các yêu cầu trước đó. Việc này dẫn tới các yếu tố như xác thực, đăng nhập, duy trì trạng thái trở nên rất bất tiện. Đó là cách các yếu tố như Cookie, JWT, SessionID ra đời. Việc thêm các header này vào HTTP request và response giúp ta dễ dàng lưu được trạng thái phiên đăng nhập và các yếu tố liên quan tới theo dõi theo thời gian thực.

Một nội dung đáng quan tâm khác của HTTP là về Proxy. Proxy có thể coi như một điểm trung gian giữa client và server trong mô hình cùng tên, proxy có nhiều tác dụng khác nhau và được sử dụng khá rộng rãi, nổi bật có thể kể đến như:
- **Chuyển tiếp (Forwarding)**: Nhận req từ client rồi gửi nó tới server. Hoặc nhận res từ server rồi trả về cho client
- **Lọc và kiểm soát (Filter)**: Chặn các site không cho phép, lọc nội dung, áp dụng các chính sách phân quyền hay giới hạn băng thông, ...
- **Ẩn danh**: Bản chất đơn giản là giấu IP thật của client, sử dụng IP proxy chứ không hoàn toàn ẩn danh
- Còn nhiều nữa, có thể kể tới như ghi log req và res, load-balancing, ...

Ứng dụng nổi bật của Proxy là web cache, lưu lại các nội dung của trang web trong những lần đầu truy cập để giảm thiểu thời gian truy cập, giảm lưu lượng truy cập web ra Internet.

## DNS - Domain Name System

Hiểu đơn giản thì Domain Name System (DNS) được ví như danh bạ của thế giới Internet, nó giúp chúng ta tìm kiếm con số đúng về địa chỉ IP chỉ bằng cách nhập tên một trang web

### Phân cấp DNS

Hệ thống tên miền được tổ chức như một cấu trúc dữ liệu cây phân cấp (hierarchical tree), bắt đầu từ gốc rễ và sau đó rẽ ra các nhánh khác nhau

- Root Servers: Đỉnh của cây phân cấp
- Top-Level Domains(TLDs): Là những phần như `.com, .org, .net` hoặc tên vùng như `.vn, .uk, .de`
- Second-level Domains: Những giá trị kiểu như example trong example.com
- Subdomains or Hostname: Những giá trị như www trong `www.example.com` hay accounts trong `accounts.google.com`

![image](https://hackmd.io/_uploads/ryT8EkYxee.png)

### DNS Resolution Process (Domain Translation)

Khi ta nhập một tên miền vào trình duyệt, máy tính cần phải tìm địa chỉ IP tương ứng right? Và quá trình trên được gọi là DNS Resolution hoặc Domain Translation. Cụ thể nó hoạt động như sau:

- Case 1: Truy vấn lặp (truy vấn tương tác hay interactive):
    - Khác với truy vấn đệ quy, trong truy vấn lặp, khi máy client yêu cầu local DNS server tìm địa chỉ IP, local DNS server sẽ không tự đi tìm đến cùng.
    - Thay vào đó, nó lần lượt hỏi từng server một (root, TLD, authoritative), nhận về địa chỉ của server tiếp theo, và trả lại thông tin cho máy client.
    - Máy client sẽ tiếp tục truy vấn các server theo gợi ý nhận được cho đến khi tìm ra địa chỉ IP cuối cùng.

- Case 2: Truy vấn đệ quy (phổ biến):
    - Step 1: Ta nhập www.anhcdex.com vào browser
    - Step 2: Máy tính kiểm tra nếu local DNS cache (bộ nhớ cục bộ) nếu đã biết về tên miền này rồi thì return luôn
    - Step 3: Nếu chưa tìm thấy ở step 2, nó sẽ gọi tới recursive DNS Server (thường của ISP cung cấp hoặc các bên thứ 3 như Google)
    - Step 4: Lời gọi đệ quy ở step 3 liên lạc tới root server, rồi từ root server nó sẽ trả về địa chỉ để ta đi đến TLD (Top-Level Domain) name server như .com hay .vn,...
    - Step 5: Từ TLD name server, nó sẽ lại điều hướng ta tới thằng Authoritative name server (DNS server có thẩm quyền) ví dụ như superanhcdex.com
    - Step 6: Authoritative name server sẽ phản hồi lại địa chỉ IP mình cần tìm
    - Step 7: Đệ quy kết thúc và trả về IP address cho máy tính của mình và kết nối tới website

Mình viết xong cũng không hiểu nó khác nhau chỗ nào, nhưng mình được dạy phân biệt nó như sau:
- Truy vấn lặp: Local DNS server liên tục hỏi từng server cấp cao xuống thấp (đi từ root xuống), nhận lại địa chỉ server tiếp theo, rồi hỏi tiếp.
- Truy vấn đệ quy: Local DNS server đẩy trách nhiệm đi hỏi các server khác, nhận lại kết quả cuối cùng

**Tóm lại, cảm giác giống nhau, nhưng khác nhau ở việc ai là người chủ động đi tìm. Ở case lặp (tương tác) thì bạn là thằng chủ động đi tìm sau từng câu hỏi còn đệ quy thì bạn hỏi 1 lần rồi đợi kết quả that's all**

### Resource Record (RR)

Cấu trúc của một bản ghi RR gồm 4 trường:
* Name: Tên của máy tính hoặc miền
* Value: Giá trị tương ứng với name, tuỳ thuộc vào type
* Type: Xác định loại bản ghi, ý nghĩa của Name và Value phụ thuộc vào Type
* TTL (Time to live): Thời gian tồn tại bản ghi

Cụ thể:
* Type A
    * Name: tên máy 
    * Value: địa chỉ IP
- Type CNAME
    - Name: bí danh của tên thật
    - Value: tên chuẩn
- Type NS
    - name: tên miền
    - value: tên host của server có thẩm quyền cho tên miền này
- Type MX
    - Value là tên của mail server được kết hợp với name

## Email

Trong tầng ứng dụng có 3 protocol chính liên quan tới email, trong đó:
- Gửi thư: SMTP - Simple Mail Transfer Protocol port 25, secured thì port 465
- Nhận thư: 
    - POP3 (Post Office Protocol) port 110 secured thì port 995, POP3 mặc định sẽ đăng nhập và lấy toàn bộ thư về
    - IMAP (Internet Mail Access Protocol) port 143, IMAP secured thì 993. IMAP cho phép quản lý thư mà không bắt buộc tải xuống

## FTP - File Transfer Protocol

FTP là 1 protocol sử dụng TCP, nó có 2 port, port 20 để truyền dữ liệu còn port 21 để điều khiển các lệnh của FTP.

Hoạt động dựa trên mô hình Client - Server, điểm khác biệt lớn nhất là tính stateful và cơ chế điều khiển out of band, nó duy trì trạng thái của user trong suốt phiên làm việc dẫn tới việc ra lệnh điều khiển có thể không nằm trong cùng 1 request

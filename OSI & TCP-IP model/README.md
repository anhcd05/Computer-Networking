# Network Concepts
> Trong bài này chúng ta sẽ bàn về các mô hình OSI, TCP/IP và một số giao thức mạng phổ biến mà đã đóng vai trò là quy tắc và chuẩn mực trong việc trao đổi thông tin trên mạng ngày nay.

## OSI model

Mô hình OSI (Open Systems Interconnection) là một mô hình mà tại đó nó chuẩn hoá các chức năng của một kết nối viễn thông hoặc một mạng máy tính thành 7 tầng khác nhau. Mô hình này giúp các nhà cung cấp dịch vụ mạng và các nhà phát triển tạo ra các thiết bị mạng và phần mềm có thể tương tác được với nhau.

### 1. **Physical Layer - Tầng vật lý**
* Là tầng đầu tiên và thấp nhất trong mô hình OSI
* Chịu trách nhiệm truyền và xử lý các dòng bit thô (không có cấu trúc) qua các đường truyền vật lý như Ethernet cables, hubs, repeaters

### 2. **Data Link Layer - Tầng liên kết dữ liệu**
* Tầng này cung cấp `nodes to nodes data transfer, which is a direct link between two physically connected nodes`
* Tầng này đồng thời đảm bảo các khối dữ liệu (data frames) được truyền đi với cùng sự đồng bộ, kiểm soát lỗi và các luồng cần thiết
* Các thiết bị như `switches, bridges` hoạt động ở tầng này, chúng sử dụng `địa chỉ MAC (Media Access Control)` để xác định các thiết bị mạng

### 3. **Network Layer - Tầng mạng**
* Tầng này xử lý việc di chuyển các gói tin, bao gồm quá trình xác định và chuyển tiếp một gói tin đi qua các routers khác nhau để tới đích
* Chịu trách nhiệm đảm bảo các gói tin được đưa tới đúng địa điểm thông qua nhiều mạng khác nhau
* `Routers` hoạt động ở tầng này, nó sử dụng `địa chỉ IP (Internet Protocol)` để xác định các thiết bị khác nhau và tìm đường đi hiệu quả nhất cho việc truyền dữ liệu
### 4. **Transport Layer - Tầng giao vận**
* Cung cấp truyền dữ liệu end-to-end, kiểm soát lỗi và kiểm soát luồng dữ liệu giữa hai thiết bị đầu cuối. Ghép kênh (Multiplexing) để nhiều ứng dụng có thể sử dụng cùng một kết nối mạng.
* Cắt/hợp dữ liệu khi cần thiết để phù hợp với đặc điểm của tầng dưới.
* Sử dụng 2 giao thức TCP (Tranmission Control Protocol) hoặc UDP (User Datagram Protocol)
### 5. **Session Layer - Tầng phiên**
* Tầng phiên quản lý các phiên giữa các ứng dụng, cụ thể nó thiết lập các kết nối sau đó duy trì và phá huỷ nó nếu cần thiết để cho phép các thiết bị giữ liên lạc bằng cái gọi là phiên.
* Đóng vai trò quan trọng trong việc đảm bảo việc truyền thông tin được diễn ra mạch lạc và tốt đẹp (nó có thể phục hồi phiên và tiếp tục nếu có xảy ra gián đoạn)
* Tầng này sử dụng session protocol và các APIs
### 6. **Presentation Layer - Tầng trình diễn**
* Chuyển đổi định dạng dữ liệu (data format translation) giữa các hệ thống khác nhau để đảm bảo khả năng tương thích.
* Hỗ trợ mã hóa và giải mã dữ liệu (Encryption & Decryption) để đảm bảo bảo mật. Nén dữ liệu (Data Compression) giúp tối ưu hóa băng thông mạng.
* Sử dụng các encryption protocols and data compression techniques
### 7. **Application Layer - Tầng ứng dụng**
* Là tầng cao nhất của mô hình OSI, cung cấp trực tiếp dịch vụ mạng tới người dùng bằng cách cho phép chia sẻ tài nguyên, truy cập tài nguyên từ xa, và các dịch vụ mạng khác
* Sử dụng HTTP, FTP, SMTP, DNS

![image](https://hackmd.io/_uploads/rJlwPVPjJx.png)

## TCP/IP Model

Mô hình TCP/IP (Transmission Control Protocol) là một phiên bản được đúc kết từ mô hình OSI. TCP/IP được điều chỉnh để có thể áp dụng vào thực tiễn trên Internet và các mạng máy tính khác.

Mô hình TCP/IP được phát triển từ thời kỳ đầu của Internet vào năm 1974, nó được thiết kế dựa trên họ giao thức cùng tên

### 1. Link Layer - Tầng liên kết
- Là tầng thấp nhất trong mô hình TCP/IP
- Chịu trách nhiệm xử lý các khía cạnh liên quan tới phần cứng của các thiết bị mạng cũng như các phương tiện truyền dẫn (Nhận IP datagram và truyền chúng)
- Tầng này bao gồm các Ethernet (wired connection) và Wi-Fi (wireless connection)
- Link Layer của TCP/IP tương ứng với Physical Layer + Data Link Layer của OSI

### 2. Internet Layer - Tầng mạng
- Tầng Internet quản lý việc đánh địa chỉ cho các thiết bị và việc định tuyến (tìm đường đi) cho các gói tin qua nhiều mạng khác nhau
- Tầng này sử dụng các giao thức như IP (Internet Protocol) và ICMP (Internet Control Message Protocol), chúng đảm bảo dữ liệu đi tới đúng nơi nó cần đến thông qua việc xác định đường đi logic trong quá trình truyền gói tin
- Tầng này tương ứng Network Layer của OSI

### 3. Transport Layer - Tầng giao vận
- Nhiệm vụ cơ bản là cung cấp các dịch vụ, phương tiện để liên lạc từ chương trình ứng dụng này tới chương trình ứng dụng khác, gọi là đầu cuối (end-to-end), thứ được họ coi là rất quan trọng trong quá trình hoạt động của Internet
- Tầng giao vận đảm bảo các gói tin được đưa đi tuần tự và không gặp lỗi
- Sử dụng TCP (Transmission Control Protocol) cho các giao tiếp cần đảm bảo sự đáng tin cậy và UDP (User Datagram Protocol) cho các giao tiếp dịch vụ cần nhanh hơn, và không cần kết nối. UDP thường được dùng cho cáp quang vì việc xảy ra lỗi là rất nhỏ nên không cần phải dùng TCP nữa

### 4. Application Layer - Tầng ứng dụng
- Là tầng cao nhất trong mô hình TCP/IP
- Chứa và quản lý các giao thức cung cấp phương tiện liên lạc, truyền thông dữ liệu cụ thể cho các ứng dụng. Hỗ trợ việc trình bày, mã hoá và quản lý cuộc gọi
- Sử dụng HTTP, FTP, SMTP, DNS
- Tương đương với Session Layer + Presentation Layer + Application Layer của OSI

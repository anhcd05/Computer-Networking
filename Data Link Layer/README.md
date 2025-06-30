# Tầng liên kết dữ liệu

**Nhắc lại các thông tin cơ bản về Data Link Layer**
- Chức năng chính: Có trách nhiệm truyền datagram (khung frame đóng gói từ các datagram) từ một nút tới một nút vật lý lân cận qua một liên kết
    - Đóng gói dữ liệu với đơn vị là frame
    - Địa chỉ hoá sử dụng địa chỉ MAC (Media Access Control)
    - Điều khiển truy nhập đường truyền
    - Phát hiện và sửa lỗi

Tầng liên kết được cài đặt tại adaptor (còn được gọi là thẻ giao diện mạng NIC - Network Interface Card) hoặc được cài trên chip

# Các giao thức MAC

- Về thứ tự xác suất đụng độ
    - Chia kênh: Vì chia kênh, mỗi nút sử dụng 1 kênh riêng nên việc đụng độ là không thể xảy ra
    - Ngẫu nhiên: Có thể xảy ra, > 0. Thứ tự giảm dần là Pure Aloha > Slotted Aloha > CSMA
    - Thẻ bài: Từng nút sử dụng các đường truyền được chia theo thẻ bài => Đụng độ = 0

## Các giao thức phân chia kênh

### TDMA - Time division multiple access Đa truy nhập phân chia theo thời gian

Mỗi nút mạng được phép truyền trong khe thời gian dành riêng cho nút mạng đó

### CDMA - Code division multiple access Đa truy nhập phân chia theo mã

### FDMA - Frequency division multiple access - Đa truy nhập phân chia theo tần suất

## Các giao thức truy cập ngẫu nhiên

Đặc điểm chung: 

### Pure Aloha
Trong phương pháp pure aloha, nút mạng sẽ truyền ngay.

### Slotted Aloha
Trong phương pháp slotted aloha, đồng bộ thời gian giữa các nút. Trong 1 frametime chỉ truyền 1 khung tin.

### CSMA - Carrier sense multiple access - Nghe trước khi truyền

### CSMA/CD - Carrier sense multiple access / collision detection - Nghe trong khi truyền
CSMA/CD có phát hiện đụng độ và thông báo cho các nút mạng. Nó vừa nghe trước khi nói và trong khi nói.


## Các giao thức xoay vòng

### Token Passing - sử dụng thẻ bài
Là gói tin có khuôn dạng và kích thước xác định
Thẻ bài được luân chuyển tuần tự qua các nút mạng
Cho phép thiết lập mức độ ưu tiên truyền dữ liệu
Chỉ tồn tại duy nhất một thẻ bài / lượt trong mạng để xác định quyền đưa dữ liệu lên đường truyền

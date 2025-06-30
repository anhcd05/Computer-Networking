
# Tầng giao vận - Transport Layer

**Nhắc lại các đặc điểm chính về tầng giao vận**
- Nhiệm vụ chính là điều khiển việc cung cấp dữ liệu giữa các tiến trình bằng cách cung cấp phương tiện truyền giữa các ứng dụng đầu cuối (end to end)
- Hai dịch vụ chính trong tầng giao vận:
    - TCP: tin cậy, hướng liên kết với đơn vị truyền là segment (Thường ứng dụng trong mail, web, tin nhắn, ...)
    - UDP: không tin cậy, hướng không liên kết với đơn vị truyền là datagram (Thường ứng dụng trong các ứng dụng cần chuyển dữ liệu nhanh, liên tục như streaming, VoIP hay voice over IP)

## Phương thức hướng liên kết (Connection-oriented)
- Trước khi truyền dữ liệu, 2 bên sẽ thiết lập một liên kết hay một session và giữ nó cố định trong suốt quá trình truyền
- Mõi packet hay segment gửi đi đều được đánh số, khi nhận được bên nhận phải xác nhận bằng gói tin ACK để báo nhận được. Nếu không thì bên gửi sẽ retransmission hay gửi lại gói tin
-  Có cơ chế phát lại, kiểm soát luồng, kiểm soát tắc nghẽn, tin cậy

## Phương thức hướng không liên kết (Connection-less)
- Gửi từng gói tin, không session, không đánh số, không xác nhận
- Độ trễ thấp, overhead rất nhỏ
- Không đảm bảo tin cậy, không kiểm soát luồng và tắc nghẽn

## UDP - User Datagram Protocol

Là một giao thức connection-less, truyền tin theo kiểu "best effort" gửi nhanh và nhiều nhất có thể và mỗi datagram (bức tin) chỉ gửi 1 lần không gửi lại

=> Ưu điểm: 
- Giảm độ trễ vì không cần thiết lập liên kết
- Đơn giản vì không cần lưu session, trạng thái, ...
- Overhead rất nhỏ (UDP mặc định 8 bytes)

UDP luôn có 8 bytes overhead, trong đó bao gồm những cái dưới đây với ý nghĩa đúng như tên gọi:
- Source port
- Dest port
- Length: 
- Checksum

Ngoài ra có một điểm khác biệt nữa của UDP so với TCP là UDP hỗ trợ broadcast/multicast tức cho phép gửi datagram tới nhiều đơn vị cùng một lúc

![image](https://github.com/user-attachments/assets/f67450fb-3cda-4883-b009-cce56707634c)

## TCP - Transmission Control Protocol

Là một giao thức connection-oriented, và cách thiết lập liên kết của TCP là bắt tay 3 bước cụ thể:
- SYN
- SYN ACK
- ACK

Ngoài ra để huỷ bỏ kết nối thì có 1 cái ngược với 3 way handshake, giang hồ gọi là 4 way teardown. À cả cái này lẫn cái trên thì các bước có flag nào thì flag đó bằng 1 nhé:
- FIN
- ACK
- FIN
- ACK

Kích thước overhead của TCP không cố định do có 1 vùng options

![image](https://github.com/user-attachments/assets/0a2f2827-957b-4999-9f92-11b854360304)

Để đảm bảo tính tin cậy, overhead của TCP khá nặng. TCP sẽ sử dụng những thứ sau để đảm bảo tính tin cậy:
- Kiểm soát lỗi: Checksum
- Kiểm soát mất mát gói tin: Timeout
- Kiểm soát dữ liệu đã nhận được chưa: Sử dụng pipeline với Seq# để gửi tuần tự kèm xác nhận ACK

Có khả năng phát hiện lỗi, sẽ báo cho bên gửi theo 2 gói tin ACK (Acknowledgements) hoặc NAK (Negative Acknowledgements), nếu gặp NAK thì bên gửi sẽ retransmission

Ngoài ra còn rất nhiều nội dung chi tiết của TCP, như cách nó kiểm soát tắc nghẽn, check lỗi, kiểm soát luồng, ... Nhưng mình thấy khá dài nên lười và cảm giác như những cái này khá khó không được hỏi nhiều

## Chồng giao thức
Một nội dung rất hay được hỏi khi thi trắc nghiệm, đó là các giao thức sử dụng UDP hay TCP. Để đơn giản hoá vấn đề này thì ta cần biết tới sơ đồ chồng giao thức của TCP/IP. Cụ thể:

![image](https://github.com/user-attachments/assets/e29fb3c0-fc5a-42e2-b825-9cbd32067f96)

# Rảnh thì bổ sung kiến thức về các trường trong overhead của TCP, ý nghĩa, nội dung, độ dài vì hỏi khá nhiều chẳng hạn như Rvcr Window, ý nghĩa của AckKnow number và SeqNumber, số byte min của TCP overhead, IP overhead để làm bài tính toán

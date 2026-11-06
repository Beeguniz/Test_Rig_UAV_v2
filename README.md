# TEST RIG UAV 3 BẬC TỰ DO (3-DOF)

## 1. Giới thiệu

Thư mục này lưu trữ tài liệu thiết kế của **Test Rig UAV 3 bậc tự do
(3-DOF)**. Hệ thống được định hướng phục vụ thử nghiệm chuyển động quay
và đánh giá đáp ứng của hệ thống điều khiển UAV quanh ba trục:

-   **Roll (φ):** quay quanh trục dọc thân UAV.
-   **Pitch (θ):** quay quanh trục ngang thân UAV.
-   **Yaw (ψ):** quay quanh trục thẳng đứng thân UAV.

Test Rig hỗ trợ tạo môi trường thử nghiệm có kiểm soát, quan sát chuyển
động, thu thập dữ liệu cảm biến và đánh giá đáp ứng điều khiển. Hệ thống
có thể được sử dụng để hỗ trợ nghiên cứu, kiểm tra và tinh chỉnh bộ điều
khiển PID.

> **Lưu ý về phạm vi:** Test Rig 3-DOF trong tài liệu này được hiểu là
> giàn thử cho phép khảo sát ba chuyển động quay Roll--Pitch--Yaw. Điều
> này không đồng nghĩa với mô phỏng đầy đủ sáu bậc tự do (6-DOF) của
> UAV, vì ba chuyển động tịnh tiến X--Y--Z không nhất thiết được tái tạo
> trên giàn.

## 2. Mục tiêu thử nghiệm

1.  Kiểm tra khả năng quay và giới hạn chuyển động quanh các trục Roll,
    Pitch và Yaw.
2.  Đánh giá phản ứng của UAV hoặc cụm điều khiển khi nhận lệnh đặt.
3.  Ghi nhận dữ liệu góc, tốc độ góc và tín hiệu điều khiển (nếu hệ
    thống đo/ghi hỗ trợ).
4.  So sánh đáp ứng khi thay đổi các hệ số PID (K_p), (K_i), (K_d).
5.  Đánh giá các chỉ tiêu như sai số, độ vọt lố, thời gian xác lập và
    mức dao động.
6.  Hỗ trợ kiểm tra trước khi tiến hành thử nghiệm bay có kiểm soát.

## 3. Cấu trúc thư mục

``` text
2D/
├── PART/     # Các chi tiết, cụm chi tiết hoặc mô hình linh kiện
├── Draw/     # Bản vẽ kỹ thuật, bản vẽ lắp và tài liệu thể hiện kích thước
└── README.md
```

Nội dung cụ thể bên trong `PART` và `Draw` cần được cập nhật theo các
tệp thực tế của dự án. Không tự ý đổi tên hoặc di chuyển tệp CAD nếu
chúng còn liên kết tham chiếu với cụm lắp ráp.

### Vai trò của Test Rig

Test Rig **không mặc nhiên tự tính ra** (K_p), (K_i), (K_d). Hệ thống
tạo điều kiện thử nghiệm và cung cấp dữ liệu để người nghiên cứu hoặc
thuật toán tuning đánh giá, điều chỉnh các hệ số. Bộ điều khiển PID
thường được thực thi trong Flight Controller; cần xác định rõ kiến trúc
thực tế của dự án trước khi kết luận tín hiệu nào được đo và xử lý ở
từng khối.
##MÔ HÌNH 3D TEST RIG UAV

### Xem mô hình 3D

[🔗 Nhấn vào đây để xem mô hình 3D trực tiếp trên GitHub](CAD/laprapfix.stl)



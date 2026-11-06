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
## Mô hình 3D Test Rig UAV

### Mô hình tổng thể

![Test Rig UAV 3D](Images/test-rig-preview.png)

### File thiết kế 3D

- [Xem mô hình 3D STL](3D/TestRig_UAV.stl)
- [Tải mô hình CAD gốc STEP](3D/TestRig_UAV.STEP)

## 4. Nguyên lý thử nghiệm PID

Bộ điều khiển PID tạo tín hiệu điều khiển từ sai số giữa giá trị đặt và
giá trị đo:

\[ e(t)=r(t)-y(t) \]

\[ u(t)=K_p e(t)+K_i`\int`{=tex}\_0\^t e(`\tau`{=tex}),d`\tau`{=tex}
+K_d`\frac{de(t)}{dt}`{=tex} \]

Trong đó:

-   (r(t)): giá trị đặt (ví dụ góc Roll/Pitch/Yaw hoặc tốc độ góc đặt).
-   (y(t)): giá trị đo từ cảm biến.
-   (e(t)): sai số điều khiển.
-   (u(t)): tín hiệu điều khiển đầu ra.
-   (K_p): hệ số tỷ lệ, quyết định mức phản ứng với sai số hiện tại.
-   (K_i): hệ số tích phân, xử lý sai số tích lũy theo thời gian.
-   (K_d): hệ số vi phân, phản ứng với tốc độ thay đổi sai số.

### Vai trò của Test Rig

Test Rig **không mặc nhiên tự tính ra** (K_p), (K_i), (K_d). Hệ thống
tạo điều kiện thử nghiệm và cung cấp dữ liệu để người nghiên cứu hoặc
thuật toán tuning đánh giá, điều chỉnh các hệ số. Bộ điều khiển PID
thường được thực thi trong Flight Controller; cần xác định rõ kiến trúc
thực tế của dự án trước khi kết luận tín hiệu nào được đo và xử lý ở
từng khối.

## 5. Quy trình thử nghiệm đề xuất

### 5.1. Kiểm tra trước khi chạy

-   Kiểm tra độ chắc chắn của khung, trục quay, ổ đỡ, khớp nối và các
    vít liên kết.
-   Kiểm tra giới hạn cơ khí của từng trục, bảo đảm không va chạm khi
    quay.
-   Kiểm tra dây điện, nguồn cấp, kết nối cảm biến và bộ điều khiển.
-   Kiểm tra khả năng dừng khẩn cấp và phương án ngắt nguồn.
-   Tháo cánh quạt trong các bước kiểm tra điện tử/hiệu chỉnh không cần
    tạo lực đẩy.
-   Chỉ lắp và vận hành cánh quạt khi giàn thử đã được thiết kế, che
    chắn và đánh giá an toàn phù hợp.

### 5.2. Kiểm tra từng bậc tự do

1.  Kiểm tra trục Roll riêng biệt trong giới hạn góc cho phép.
2.  Đưa hệ thống về vị trí tham chiếu, sau đó kiểm tra trục Pitch.
3.  Kiểm tra trục Yaw và xác nhận chiều dương/chiều âm.
4.  Kiểm tra phối hợp nhiều trục ở mức lệnh nhỏ, sau khi từng trục đã
    hoạt động đúng.
5.  Ghi lại hiện tượng rung, ma sát, độ rơ, va chạm hoặc sai lệch cảm
    biến.

### 5.3. Thử nghiệm và đánh giá PID

-   Ghi lại bộ thông số PID ban đầu và phiên bản firmware/cấu hình sử
    dụng.
-   Xác định rõ đang điều khiển **góc (Angle/Attitude)** hay **tốc độ
    góc (Rate)**.
-   Đặt lệnh thử nghiệm nhỏ, có giới hạn và lặp lại được.
-   Ghi đồng bộ giá trị đặt, giá trị đo, thời gian và tín hiệu điều
    khiển.
-   Thay đổi thông số có kiểm soát; ưu tiên thay đổi từng hệ số hoặc
    từng nhóm theo một kế hoạch tuning rõ ràng.
-   So sánh kết quả trước và sau hiệu chỉnh.

## 6. Dữ liệu nên ghi nhận

  -----------------------------------------------------------------------
  Nhóm dữ liệu            Đại lượng gợi ý         Mục đích
  ----------------------- ----------------------- -----------------------
  Lệnh đặt                Roll/Pitch/Yaw hoặc tốc Xác định yêu cầu điều
                          độ góc đặt              khiển

  Cảm biến                Góc, tốc độ góc, gia    Đánh giá phản ứng thực
                          tốc góc                 tế

  Điều khiển              PID output, motor       Kiểm tra tín hiệu điều
                          command, RPM (nếu có)   khiển

  Thời gian               Timestamp, sampling     Phân tích đáp ứng theo
                          rate                    thời gian

  Cấu hình                PID, firmware, filter,  Bảo đảm khả năng tái
                          chế độ bay              lập thử nghiệm
  -----------------------------------------------------------------------

Các chỉ tiêu đánh giá có thể gồm:

-   **Sai số:** (e(t)=r(t)-y(t)).
-   **RMSE:** căn bậc hai của trung bình bình phương sai số.
-   **Overshoot:** mức vượt quá giá trị đặt.
-   **Settling time:** thời gian để đáp ứng đi vào và duy trì trong dải
    sai số quy định.
-   **IAE:** tích phân sai số tuyệt đối theo thời gian.

## 7. Thông tin dự án cần bổ sung

Để README phản ánh chính xác cấu hình thực tế, nhóm thiết kế cần điền
các thông tin sau:

  Hạng mục                     Thông tin
  ---------------------------- ----------------------------------------------
  Tên/mã Test Rig              \[Bổ sung\]
  Phần mềm thiết kế CAD        \[Bổ sung tên và phiên bản\]
  Flight Controller            \[Bổ sung model\]
  Firmware                     \[INAV/PX4/ArduPilot/khác -- ghi phiên bản\]
  Cảm biến                     \[IMU/Gyroscope/Encoder và model\]
  Cơ cấu chấp hành             \[Motor/servo/ESC và model\]
  Phạm vi góc Roll             \[Bổ sung\]
  Phạm vi góc Pitch            \[Bổ sung\]
  Phạm vi góc Yaw              \[Bổ sung\]
  Tần số lấy mẫu/ghi dữ liệu   \[Bổ sung\]
  Phần mềm phân tích dữ liệu   \[Bổ sung\]

Không điền thông số khi chưa đo, kiểm tra hoặc xác nhận từ thiết kế.

## 8. An toàn

-   Không đưa tay hoặc vật thể vào vùng chuyển động của giàn khi hệ
    thống đang cấp nguồn.
-   Cố định Test Rig trên bề mặt đủ cứng vững trước khi thử nghiệm.
-   Có giới hạn cơ khí hoặc giới hạn phần mềm phù hợp cho từng trục.
-   Bố trí nút dừng khẩn cấp/ngắt nguồn trong tầm với của người vận
    hành.
-   Kiểm tra rung động, độ rơ và khả năng chịu tải trước khi tăng mức
    thử nghiệm.
-   Nếu sử dụng cánh quạt, phải có biện pháp che chắn và vùng cách ly
    phù hợp; không đứng trong mặt phẳng quay của cánh quạt.
-   Không xem kết quả thử trên Test Rig là bằng chứng duy nhất chứng
    minh UAV an toàn khi bay tự do.

## 9. Quản lý phiên bản và kết quả

Mỗi lần thử nghiệm nên lưu:

-   Ngày giờ thử nghiệm và người thực hiện.
-   Mã cấu hình cơ khí/phiên bản CAD.
-   Flight Controller, firmware và cấu hình PID.
-   Điều kiện thử, lệnh đầu vào và giới hạn an toàn.
-   Tệp dữ liệu thô và kết quả phân tích.
-   Các thay đổi đã thực hiện và kết luận.

Đặt tên tệp dữ liệu theo quy tắc thống nhất, ví dụ:

``` text
YYYYMMDD_Axis_Mode_PIDVersion_RunNumber.csv
```

Ví dụ: `20261106_ROLL_RATE_PIDv01_Run01.csv`.

------------------------------------------------------------------------

**README này là tài liệu giới thiệu và hướng dẫn khung cho dự án.** Các
thông số cơ khí, điện, firmware, giới hạn góc và quy trình vận hành
chính thức phải được cập nhật theo thiết kế và kết quả kiểm tra thực tế
của Test Rig.


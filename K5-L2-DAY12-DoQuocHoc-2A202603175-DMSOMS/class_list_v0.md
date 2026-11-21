# Danh sách lớp v0 — Đỗ Quốc Học · G01

Viết tiếp từ slide 54 bài giảng. Mỗi lớp trả lời: **model cần nhận ra cái này để làm gì?**

## DMS (7 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` (`seat = driver`, `seatbelt`) | `worn_correct` / `worn_incorrect` / `not_worn` / `unknown` | Kiểm tra tài xế có ngồi đúng vị trí và thắt dây an toàn đúng cách để cảnh báo an toàn | Có (dạng tổng thể người và dải dây; dễ bị che trong vùng tối hoặc áo tối màu) |
| 2 | `face` (`eye_left`, `eye_right`) | `open` / `closed` / `unknown` | Theo dõi tỉ lệ nhắm mắt (PERCLOS) và chớp mắt bất thường để cảnh báo buồn ngủ | Có, trừ khi tròng kính bị đốm phản xạ LED NIR hoặc mắt bị tay/tóc che |
| 3 | `face` (`glasses`) | `none` / `clear` / `sun` / `unknown` | Nhận biết tài xế đeo kính cận hay kính râm để model hiểu giới hạn quan sát vùng mắt và điều chỉnh ngưỡng cảnh báo | Hạn chế: trên NIR một số kính râm có thể trông hơi trong suốt nên dễ nhầm với kính cận |
| 4 | `face` (`gaze_zone`) | `road` / `mirror_l` / `mirror_r` / `mirror_c` / `cluster` / `center` / `lap` / `other` | Xác định vùng tài xế đang nhìn để phát hiện mất tập trung (nhìn màn hình trung tâm hoặc đùi quá lâu khi xe chạy) | Có, dựa theo hướng đầu và vị trí đồng tử khi không bị lóa kính |
| 5 | `face13` (13 điểm mặt) | 8 điểm mắt, 1 chóp mũi, 4 điểm miệng (kèm cờ `occluded` / `outside`) | Ước lượng tư thế đầu 3D (yaw, pitch, roll), độ mở mắt (EAR) và độ mở miệng (ngáp) | Có với khoảng cách gần và đủ sáng NIR; điểm sau vật che cần đánh dấu `occluded` |
| 6 | `hand` (`whose`, `side`, `on_wheel`) | `driver` / `passenger`, `left` / `right`, `yes` / `no` / `unknown` | Kiểm tra tài xế có cầm vô lăng hay đang rời tay làm việc khác (hỗ trợ bàn giao quyền điều khiển ở xe tự lái) | Có (hình dạng bàn tay và vị trí so với vành vô lăng nhìn rõ trên NIR) |
| 7 | `phone` (`state`) | `held` / `mounted` / `lap` | Phát hiện tài xế cầm hoặc nhìn điện thoại (hành vi gây mất tập trung nghiêm trọng), phân biệt với điện thoại gắn trên giá | Có về hình dạng/màn hình sáng, nhưng dễ nhầm với vật tối hình chữ nhật khác nếu bị tay che |

## OMS (7 lớp)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | `person` (`seat`) | `rear_left` / `rear_middle` / `rear_right` (và hàng trước nếu có) | Đếm số hành khách và biết chính xác ghế nào có người ngồi để kích hoạt cảnh báo hoặc điều chỉnh túi khí/điều hòa | Có (hình dạng cơ thể nhận diện rõ, nhưng màu áo không phân biệt được) |
| 2 | `person` (`seatbelt`) | `worn_correct` / `worn_incorrect` / `not_worn` / `unknown` | Cảnh báo hành khách hàng ghế sau chưa thắt dây an toàn hoặc thắt sai (luồn dưới nách/sau lưng) | Hạn chế: dây an toàn dễ chìm vào áo tối màu hoặc bóng tối góc cabin |
| 3 | `face` (OMS box) | box mặt hành khách | Định vị vùng đầu hành khách để ước lượng tư thế ngồi (ngả quá mức, cúi thấp) và phân biệt người với đồ vật | Có (hình dạng đầu/mặt tương đối rõ dù thiếu thông tin màu sắc) |
| 4 | `child_seat` (`seat`, `occupied`) | `occupied`: `no` / `unknown` | Nhận diện ghế trẻ em lắp cố định theo từng ghế để nhắc kiểm tra trẻ bị bỏ quên trên xe và tránh báo nhầm hành khách người lớn | Có (hình dáng ghế nổi rõ), nhưng khó xác định có vật/trẻ nhỏ bên trong nếu bị thành ghế che (`unknown`) |
| 5 | `infant_seat` (`seat`, `facing`) | `facing`: `rear` / `front` | Phân biệt nôi xách em bé quay ngược hay quay xuôi nhằm vô hiệu hóa túi khí tương ứng và cảnh báo quên trẻ | Có (hình dáng nôi và hướng quay đầu ghế thường phân biệt được) |
| 6 | `object` (`seat`, `type`) | `bag` / `box` / `cup` / `other` | Tránh cảnh báo nhầm đồ vật nặng đặt trên ghế là hành khách chưa thắt dây an toàn; phát hiện vật dụng để quên trên ghế | Có về hình dạng khối (túi, hộp, cốc), nhưng chi tiết vật liệu/chữ in khó nhận biết nên dễ phải chọn `other` |
| 7 | `frame_meta` (`modality`, `light`, `camera_blocked`) | `rgb` / `ir`, `day` / `night` / `unknown`, `yes` / `no` | Phân loại luồng dữ liệu ngày/đêm/RGB/IR và phát hiện camera bị che khuất để pipeline loại khung hỏng hoặc chuyển mô hình phù hợp | Có (`camera_blocked` phát hiện qua vùng mất tín hiệu hoặc vật sát ống kính) |

## 2 câu hỏi leo thang

Câu hỏi bạn muốn hỏi người viết guideline (hoặc khách hàng) vì guideline v1.0 chưa trả lời. Mỗi câu kèm **tên khung** làm ví dụ.

1. Câu hỏi: `GUIDE.md` §3 nêu *"SVIRO: Bộ ảnh không có trẻ em ngồi. Thấy hình giống trẻ em thì báo coach, không gán"*, và schema `child_seat.occupied` chỉ cho phép `no` hoặc `unknown` (không có `yes`). Tuy nhiên trong gói ảnh `G01/oms/` có tới **5/8 cảnh** (`S02`, `S03`, `S05`, `S07`, `S08`) có trẻ em hoặc em bé ngồi trong ghế trẻ em/nôi xách. Vậy với các cảnh này, model OMS có cần bổ sung nhãn `child_seat.occupied = yes` và gán thêm `person` + `face` cho trẻ nhỏ hay chỉ khoanh box ghế?  
   Khung ví dụ: `S02_rgb`, `S02_ir`, `S03_rgb`, `S03_ir`, `S05_rgb`, `S05_ir`, `S07_rgb`, `S07_ir`, `S08_rgb`, `S08_ir` (ví dụ tiêu biểu: `S05_ir` có hai trẻ em ngồi trong `child_seat` ở `rear_right` và `rear_left`; `S02_ir` có em bé nằm trong `infant_seat` ở `rear_right`).  
   Bạn tạm gán thế nào và vì sao: Thực hiện đúng `GUIDE.md` §3 và thống nhất quy tắc xử lý tại chỗ: chỉ gán hộp `child_seat` (`occupied = unknown` vì không có giá trị `yes`) và `infant_seat` (`facing = rear` trên `S02`, `facing = front` trên `S07` và `S08`), **không gán `person` hay `face` cho trẻ em/em bé**, đồng thời liệt kê đủ 5 cảnh vào danh sách báo coach.
2. Câu hỏi: Trên ảnh NIR thật của DMS, khi ánh sáng hồng ngoại hoặc trang phục tạo vùng bất định — chẳng hạn đốm phản xạ LED đè đúng lên tròng kính một phần (`D02`, `D05`), bàn tay bị cháy sáng trắng xóa mất kết cấu (`D06`), hoặc áo khoác tối màu che vùng vai ngực khi tài xế nghiêng người (`D01`) — ngưỡng thấy bao nhiêu phần trăm khe mí mắt hay dải dây an toàn thì được chuyển từ `unknown` sang `open`/`closed` hoặc `worn_correct`?  
   Khung ví dụ: `D01` (áo khoác đen che ngang ngực, không thấy rõ dải chéo qua thân trên), `D02` & `D05` (đốm phản xạ LED NIR trên tròng kính cận), `D06` (bàn tay trái bị bão hòa trắng xóa trên ảnh NIR).  
   Bạn tạm gán thế nào và vì sao: Tuân thủ Quy tắc 1 (*"Không thấy thì `unknown`"*): với `D01` giữ `person.seatbelt = unknown` thay vì đoán theo các khung `D02`–`D06`; với `D02` và `D05` gán `eye_left = unknown`, `eye_right = unknown` và bật cờ `occluded` tương ứng trên `face13`; với `D06` dùng ranh giới vòng cổ tay để khoanh `hand` bị cháy sáng và chỉ gán `closed` ở mắt do không đeo kính (`glasses = none`) và nhìn rõ hai mí khép.

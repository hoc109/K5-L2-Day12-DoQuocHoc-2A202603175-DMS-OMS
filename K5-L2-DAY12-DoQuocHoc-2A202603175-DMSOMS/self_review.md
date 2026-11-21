# Tự đánh giá — Đỗ Quốc Học · G01

## 1. Tự rà soát 4 cảnh

Mở lại bài của mình, chọn 4 ảnh (2 S##, 2 D##), đọc như người lạ.

Loại lỗi: `seat_flip`, `wrong_class`, `guess`, `box`, `missing`, `extra`, `lr_flip` (trái/phải mặt), `flag` (thiếu cờ điểm), `ok`.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| `S01_rgb` / `S01_ir` | `child_seat` (`rear_left`), `infant_seat` (`rear_right`) | `guess` / `ok` | Ban đầu dễ copy nhãn `occupied=no` từ IR sang `S01_rgb`; rà lại `S01_rgb` thấy lòng ghế chìm trong bóng tối sâu nên sửa thành `occupied=unknown` theo Quy tắc 1 | Rồi |
| `S06_rgb` / `S06_ir` | `object` (`rear_middle`), `infant_seat` (`rear_left`) | `guess` / `ok` | Trên `S06_rgb` ba lô chìm trong bóng tối nên ghi `type=other`; trên `S06_ir` nhìn rõ quai và khóa kéo nên ghi `type=bag`. Ánh xạ ghế theo xe (`rear_right` trái ảnh, `rear_left` phải ảnh) đúng | Rồi |
| `D04` | `face13` (`nose_tip`, miệng), `person` | `box` / `flag` | Khi soi lại overlay phóng to phát hiện `nose_tip` và cụm điểm miệng bị lệch sang trái khoảng 20 px vào vùng nền tối, đồng thời cạnh phải box `person` cắt nhẹ phần chỏm tóc tối màu | Rồi |
| `D06` | `hand` (`left`, `right`), `face` (`glasses`, `eye_*`) | `ok` | `glasses=none` đúng quy tắc (kính cầm trên tay); phân biệt rõ tay trái cháy sáng trắng xóa dưới đèn NIR (cắt theo vòng cổ tay) với tay phải cầm kính; hai mắt thấy rõ mí khép nên ghi `closed` | Rồi |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

Lỗi: Cắt chặt cạnh phải khung `person` trên ảnh D## (chừa thiếu phần đỉnh đầu/tóc chìm trong nền tối) và đặt lệch nhóm điểm mũi/miệng trên `face13` khi mặt tài xế nghiêng góc lớn (`D01`, `D03`, `D04`).

Vì sao mình mắc: Ảnh NIR tương phản tối ở vùng rìa ghế dựa và đầu tài xế; trên ảnh xoay 90° rất dễ đọc nhầm trục `x` nhỏ/lớn hoặc ước lượng nhanh khi không phóng to tăng sáng tạm trên viewer.

Lần sau tránh bằng cách: Tăng sáng/tương phản hiển thị tạm thời trên CVAT khi kiểm cạnh box vùng tối và rà từng điểm `face13` trên vùng zoom trước khi export checkpoint.

## 3. Ghi chú về disagreement_log

Một dòng bạn của mình đúng và mình sai. Mình học được gì từ dòng đó: Ở dòng `D04.png | hand | box` (`IoU=0.38`, tay trái `side=left`), hộp ở bản `export_final.zip` bị lệch và cắt thiếu phần đầu ngón/cổ tay trong vùng tối, trong khi hộp của bạn (`bachtuan2612`) ôm sát bàn tay hơn; ngoài ra ở dòng `D04.png | face | box` (`IoU=0.49`) cả hai bản v1 và peer đều lệch nhẹ (bản của mình hụt cằm `x1=1008`, bản peer cắt thiếu tai `y2=466`). Từ các đối chiếu này, mình đã chỉnh lại biên hộp tay trái, hộp `face` và tinh chỉnh lại các điểm `face13` trên CVAT (nhờ đó `export_final_v2.zip` đạt `0 lỗi, 0 cảnh báo` ở `check_final_v2.txt`), đồng thời rèn thói quen đối chiếu kỹ phần rìa tối trước khi chốt box.

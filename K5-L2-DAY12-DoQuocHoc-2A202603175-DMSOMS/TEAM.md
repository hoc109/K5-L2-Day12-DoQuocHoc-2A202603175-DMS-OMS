# TEAM — Ngày 12

Mã bộ ảnh: **G01** · Hình thức: cá nhân (review chéo với bạn cùng mã G01)

| Họ tên | MSSV | Đã gán đủ 22 ảnh? | Review chéo với (peer diff) | Số dòng disagreement đã xử lý |
|---|---|---|---|---|
| Đỗ Quốc Học | 2A202603175 | có | `bachtuan2612` - Bạch Đăng Ngọc Tuấn | 103 |
| | | | | |

Cả hai chưa thống nhất (ghi tên ảnh + đối tượng):

- **5/8 cảnh SVIRO có trẻ em/em bé trong ghế (`S02`, `S03`, `S05`, `S07`, `S08`) — `infant_seat` / `child_seat` (`ambiguous`):** `GUIDE.md` §3 ghi bộ ảnh không có trẻ em ngồi (thấy giống trẻ em thì báo coach, không gán) và `child_seat.occupied` chỉ có `no`/`unknown`; bản mình giữ box ghế (`occupied=unknown` / đúng `facing`, không gán `person`), còn bản bạn (`bachtuan2612`) bỏ box `infant_seat` trên `S02, S07, S08` và thử ghi `occupied=yes` trên `S03, S05`. Cần coach xác nhận quy chuẩn.
- **`D04.png` — `face13.right_eye_*` & `mouth_right` ở góc mặt nghiêng (`ambiguous`):** Bản mình giữ `occluded=1, outside=0` (đoán được theo gọng kính), bản bạn chọn `occluded=0, outside=1` do mắt phải khuất hẳn. Cần coach chốt ranh giới `occluded` vs `outside`.
- **`S06_rgb.png` — `object` (`rear_middle`) ở vùng tối (`ambiguous`):** Bản mình giữ `type=other` trên RGB tối (chỉ ghi `bag` trên `S06_ir`), bản bạn ghi `bag` trên cả hai; cũng như `D02.png` `face.gaze_zone` (`road` vs `other`).

## Cá nhân

### DoQuocHoc-2A202603175
- Phần mình làm: Hoàn thành Task 0, Task 1 (`S01`–`S08`), Task 2 (`D01`–`D06`), Checkpoints A/B/Final, `ir_log.csv` (E4), `class_list_v0.md` (E5); chạy `cabin_check.py diff` đối chiếu toàn bộ 103 dòng giữa `export_final.zip` và `peer_export_final.zip` (`bachtuan2612`) thành `disagreement_log.csv` (E3), tự rà sửa thành `export_final_v2.zip` (`0 lỗi, 0 cảnh báo` ở `check_final_v2.txt`), tổng hợp ca hỏi coach và hoàn thiện `self_review.md`.
- Điều mình học được hôm nay: Phân biệt rõ bản chất giữa IR mô phỏng (SVIRO) với NIR thật (Drive&Act: đốm phản xạ LED trên tròng kính, cháy sáng tay ở cự ly gần), áp dụng đúng quy tắc gọi ghế theo xe (`rear_right` bên trái ảnh OMS), gọi trái/phải theo người trên ảnh D## xoay 90°, thói quen chọn `unknown` thay vì đoán, và tầm quan trọng của đối chiếu chéo để phát hiện lỗi biên hộp (`D04` tay trái, mặt) mà tự kiểm đơn lẻ dễ bỏ sót.

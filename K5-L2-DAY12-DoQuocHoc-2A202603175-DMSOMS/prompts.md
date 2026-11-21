# Khai báo dùng AI — Đỗ Quốc Học

Không đưa ảnh cabin hay ảnh tài xế (kể cả ảnh chụp màn hình) cho bất kỳ công cụ AI nào.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Antigravity AI | Đọc tài liệu Day 12 (`README.md`, `GUIDE.md`, `RULES.md`, `CHECKPOINTS.md`, `RUBRIC.md`, `SUBMISSION.md`, `scripts/cabin_check.py`) để tóm tắt quy trình, schema và các quy tắc tự kiểm. | Nắm nhanh quy tắc gán nhãn OMS/DMS, cấu trúc file nộp và lệnh kiểm tra cho từng checkpoint. | Có, đối chiếu trực tiếp với `GUIDE.md`, `RULES.md` và `scripts/cabin_schema.py`. |
| 2 | Antigravity AI | Soạn nội dung `class_list_v0.md` (E5), `ir_log.csv` (E4), `self_review.md`, `TEAM.md`, cùng giải thích cảnh báo `D02.png` ở cuối `check_cpB.txt` và `check_final.txt`; giữ trống `exit_ticket.md`. | Dùng làm bản báo cáo thực hành và danh sách câu hỏi leo thang gửi coach; phần `exit_ticket.md` sinh viên tự làm độc lập. | Có, rà lại từng dòng quan sát so với 22 khung hình `G01` và giữ nguyên 3 câu `exit_ticket.md` trống để tự điền. |
| 3 | Antigravity AI | Chạy `scripts/cabin_check.py check` cho `export_final_v2.zip` (`check_final_v2.txt`), chạy `scripts/cabin_check.py diff` với `peer_export_final.zip`, hỗ trợ phân loại đủ 103 dòng `disagreement_log.csv` (`verdict`, `guideline_rule`, `action`) theo Guideline Cabin v1.0 và cập nhật `self_review.md`, `TEAM.md`. | Hoàn thiện bộ bằng chứng E1–E3 sau khi sinh viên tự sửa nhãn trên CVAT local và export `export_final_v2.zip`. | Có, đối chiếu từng phán quyết với `GUIDE.md` §§3–4, kết quả `check_final_v2.txt` (`0 lỗi, 0 cảnh báo`), và tự kiểm tra lại `TEAM.md` / `exit_ticket.md`. |

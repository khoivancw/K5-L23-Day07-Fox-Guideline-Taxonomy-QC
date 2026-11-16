# Thông tin nhóm

- Tên nhóm: Fox
- Repo bài nộp (URL): https://github.com/khoivancw/K5-L23-Day07-Fox-Guideline-Taxonomy-QC
- Commit chốt bài (hash): 1e53d9d
- Số thành viên: 3  → số người gán mỗi ảnh (K): 2

| STT | MSHV | Họ và tên | Lớp (L2 / L3 / khác) | Tài khoản GitHub |
|---|---|---|---|---|
| 1 | 101 | Lê Văn Khởi | L2 | |
| 2 | 102 | Vũ Hoàng Nam | L2 | |
| 3 | 103 | Vũ Tiến Vinh | L2 | |

Danh sách trên phải khớp dòng tiêu đề của `README.md` (đã đổi theo [SUBMISSION.md](SUBMISSION.md)) và `--members` đã dùng ở `scripts/split_assign.py`.

## Phân công (mỗi người làm gì ngoài phần gán nhãn)

| MSHV | Phụ trách thêm |
|---|---|
| 101 | Soạn thảo & hoàn thiện guideline v1.0, chạy split_assign |
| 102 | Tạo project và quản lý cấu hình bộ nhãn trên CVAT |
| 103 | Phụ trách kiểm thử QC chính và chạy check_submission |

## Kết quả tóm tắt (điền cuối bài)

- Số thành viên / số lần gán mỗi ảnh (K): 3 / 2
- IAA trước calibration: IoU trung bình 0.857 , đồng thuận lớp 97.5 % (mẫu số: 321 cặp box ghép)
- Số ảnh phải calibration: 35 / 40
- Tỉ lệ lỗi sau calibration: 0.0 % theo ảnh (0/40), 0.0 % theo đối tượng (0/512)
- **Quyết định:** Release — lý do một dòng: Tỉ lệ ảnh lỗi 0.0% <= 2%, không có lỗi hệ thống, IAA đạt chuẩn IoU 0.857 và Class agreement 97.5%.

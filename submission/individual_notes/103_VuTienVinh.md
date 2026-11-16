# Ghi chú cá nhân — 103 - Vũ Tiến Vinh

## 1. Pha 1: ba ca khó tôi tìm ra trong 40 ảnh

| Ảnh | v0 không trả lời được gì | Quyết định ban đầu của tôi |
|---|---|---|
| `img_002.jpg` | Xe chở xe có cần gán riêng từng ô tô trên sàn không? Box xe chuyên chở có bao phần xe hàng nhô cao không? | Bản cá nhân ban đầu đề xuất một box `truck` cho xe chuyên chở và box riêng cho từng xe thật trên sàn. Đây là điểm khác với bản thống nhất v1.0 và là ca tôi đã hỏi lại khi gán. |
| `img_032.jpg` | Nhiều người đứng sát nhau thì gán một box chung, từng người hay `ignore_region`? Người nhìn qua kính có được gán không? | Tách từng `person` nếu nhận dạng và phân biệt được, chiều cao phần nhìn thấy từ 20 px; chỉ dùng ignore cho phần cụm không thể tách nhất quán. Không gán hình phản chiếu. |
| `img_035.jpg` | Xe ba bánh chở hàng cao có đổi lớp không, và bbox có phải bao hết bao tải/hàng hóa không? | Bản cá nhân dùng lớp `tuk_tuk`; box theo kết cấu xe, không mở lên theo hàng rời. Khi áp dụng bản nhóm, đổi tên lớp tương ứng thành `three_wheeler`. |

## 2. Pha 2: chỗ tôi bất đồng với nhóm

- Khi đối chiếu bản cá nhân với v1.0, khác biệt rõ nhất là `img_002`: bản của tôi tách xe trên sàn, còn nhóm chốt một box `truck`, không gán các ô tô hàng riêng. Tôi dùng bản thống nhất làm căn cứ cho Pha 3. Riêng cách hiểu biên box khi xe hàng nhô cao vẫn cần được nhóm xác nhận rõ trong calibration.
- Bản cá nhân tách `tuk_tuk`, `cyclo` và coi mô tô sidecar là `motorcycle`; v1.0 gom các cấu hình ba bánh vào `three_wheeler`. Tôi cần theo tên lớp chính thức của nhóm khi chọn nhãn trên CVAT.
- Ngưỡng che của bản cá nhân khác bản nhóm. V1.0 dùng mức `0`: 0–10%, `1`: trên 10–35%, `2`: trên 35–70%, `3`: trên 70% đến khoảng 85%. Không dùng lại ngưỡng 25%/75% của bản cá nhân khi gán theo v1.0.

## 3. Pha 3: ảnh tôi đã gán

- Số ảnh được giao và đã xuất: **27 ảnh**, khớp `submission/qc/assignments/103.txt`; làm trên CVAT local, task `22`, job `22`.
- File kết quả: [`103_VuTienVinh.json`](../labels/103_VuTienVinh.json), xuất COCO 1.0, hiện có **325 bbox**: `person` 184, `motorcycle` 66, `car` 40, `bicycle` 16, `three_wheeler` 9, `truck` 4, `van` 3, `bus` 3. Đây là số box trong bản export, chưa phải số đối tượng đã được QC xác nhận đúng.
- Trạng thái `can_review` trong file cuối: **3 box bật**, tại `img_007` (truck, ID 65), `img_014` (person, ID 109), `img_040` (car, ID 321); 322 box còn lại không bật. File export không ghi lịch sử thao tác nên không xác định được tổng số lần tôi tick/bỏ tick trong lúc làm.
- Các câu hỏi tôi đã đặt khi gán: xe chở xe có bao cả xe hàng không; nhiều người đứng cạnh nhau phải tách thế nào; xe ba bánh chở đồ có bao hàng không; phân biệt `occluded_level` với `truncated`. Tôi hiểu box chồng nhau không tự chứng minh cơ thể bị che, còn chạm mép ảnh cũng chưa chắc là bị cắt.
- Đã chạy `python scripts/validate_labels.py submission/labels/103_VuTienVinh.json`: **0 lỗi, 2 cảnh báo**. Hai box cao 16 px cần rà lại: `img_002` (van, ID 3) và `img_003` (person, ID 7). Chưa ghi nhận đã sửa các cảnh báo này; validator cũng không xác nhận độ sát box, đúng lớp hay bỏ sót trên ảnh.

## 4. Pha 4–5: tôi lệch ở đâu

- Tại thời điểm viết ghi chú, repo chưa có `iaa_summary.md`, `calibration_candidates.csv` hoặc `calibration_decisions.csv`; chưa thể kết luận tôi lệch ở ảnh nào, nguyên nhân gì hay đã đạt IAA.
- Những vấn đề cần mang vào calibration: biên box xe chở xe ở `img_002`, cách xử lý hàng rời trên xe ba bánh, người đứng sát nhau, ba box đang có cờ review và hai cảnh báo dưới ngưỡng 20 px. Đây là danh sách cần kiểm tra, chưa phải bất đồng đã được đo với người khác.
- Tôi cho rằng quyết định quan trọng là thống nhất một cách vẽ cho cùng loại ca và ghi thành quy tắc có ví dụ; kết quả họp thực tế và phiên bản v1.1 sẽ bổ sung sau khi nhóm thực hiện.

## 5. Dùng AI
- Không dùng AI để gán nhãn .

## 6. Bài học

- Lần sau tôi sẽ chốt sớm ví dụ về xe chở xe, xe ba bánh chở hàng và đám đông, đặc biệt ranh giới giữa kết cấu xe với hàng rời, để giảm lưỡng lự trong lúc gán.
- Tôi cần giữ riêng bản cá nhân và bản thống nhất, dùng đúng ngưỡng thuộc tính của phiên bản đang áp dụng; phân biệt kết quả kiểm tra cấu trúc với kết quả QC bằng mắt.
- Khi báo cáo tiến độ, tôi sẽ ghi số liệu từ file thực tế, giữ lại ca cần review và chỉ điền IAA/calibration sau khi nhóm đã đo, xem ảnh và chốt quyết định.

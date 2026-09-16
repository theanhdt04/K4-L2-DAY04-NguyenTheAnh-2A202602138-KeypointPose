# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: **Nguyễn Thế Anh** Nhóm: **\_\_** Ngày: **16/09/2026**

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số                       |            Giá trị |
| ---------------------------- | -----------------: |
| Số ảnh đã gán                |                 20 |
| Số skeleton                  |                 29 |
| v=2 / v=1 / v=0              |     331 / 134 / 28 |
| Thời gian trung bình mỗi ảnh | 4 phút 45 giây/ảnh |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1. **left_ear – 62%**
2. **right_ear – 52%**
3. **left_eye – 38%** _(đồng hạng với `right_eye` – 38%)_

Không hoàn toàn. Bảng đếm cao ở tai và mắt, nhưng lúc gán tôi thấy tai bị tóc hoặc vật che khó hơn vì không biết nên chọn `v=1` hay `v=2`. Ví dụ, ở `train_07`, người đứng giữa có khớp `left_hip` không nhìn thấy rõ nên tôi phải ước lượng vị trí theo phần cơ thể liền kề; hông khó vì phải đoán vị trí, còn tai khó vì phải chọn cờ.

<!-- Trả lời 2–4 câu. Phân biệt “hay bị che” với “khó xác định vị trí giải phẫu”; nêu bằng
chứng nhìn thấy thay vì chỉ nêu cảm giác. -->

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số                | Trước rework | Sau rework |
| --------------------- | -----------: | ---------: |
| OKS trung bình        |        0.943 |      0.949 |
| OKS@0.50              |        1.000 |      1.000 |
| OKS@0.75              |        1.000 |      1.000 |
| Lỗi `dao_trai_phai`   |            0 |          0 |
| Lỗi `nham_nguoi`      |            2 |          0 |
| Lỗi `xoa_khop_bi_che` |            0 |          0 |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->

- `train_01.jpg` + người #2 + `right_wrist`: kéo lại keypoint bị chấm nhầm sang cơ thể bên cạnh.
- `train_04.jpg` + người #1 + `left_wrist`: kéo lại keypoint bị chấm nhầm sang người bên cạnh.
- `train_19.jpg` + người #2 + `right_wrist`: kéo keypoint bị trượt hẳn khỏi vị trí khớp về đúng cổ tay.

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?

Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.

<!-- Nếu không có lỗi, ghi rõ “Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.” -->

## 3. Kiểm chéo

Bạn cùng nhóm: **\_\_**

Khớp lệch `%v=1` nhiều nhất giữa hai bảng đếm:

| Khớp | Bạn |  Họ | Lệch | Nguyên nhân (guideline hay gán sai?) |
| ---- | --: | --: | ---: | ------------------------------------ |
|      |     |     |      |                                      |
|      |     |     |      |                                      |

Luật mới đã bổ sung vào `GUIDELINE_MINI.md` sau khi thống nhất:

<!-- Viết một rule kiểm chứng được: điều kiện nhìn thấy/căn cứ vị trí → chọn v=1 hoặc v=0.
Không chỉ ghi “cẩn thận hơn khi gán”. -->

## 4. Model

<!-- Chép số từ outputs/eval_model.json sau Chặng 6. “Chênh” = sau fine-tune trừ baseline;
đây là quan sát trên tập test, không phải chất lượng sản phẩm. -->

| Chỉ số         | yolo26n-pose gốc | Sau fine-tune |   Chênh |
| -------------- | ---------------: | ------------: | ------: |
| pose_mAP50     |           0.8450 |        0.8450 | +0.0000 |
| pose_mAP50-95  |           0.6853 |        0.6908 | +0.0055 |
| pose_precision |           0.9734 |        0.9792 | +0.0058 |
| pose_recall    |           0.8462 |        0.8462 | +0.0000 |
| box_mAP50-95   |           0.8119 |        0.8041 | -0.0078 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` tăng `0.0055`, từ `0.6853` lên `0.6908`; đây là mức tăng nhỏ trên tập test 10 ảnh. Hai mươi ảnh train giúp model thích nghi thêm với các tư thế, góc nhìn và quy tắc đặt keypoint/visibility của bộ ảnh này, nhưng chưa đủ để kết luận model tốt hơn nói chung; `box_mAP50-95` lại giảm `0.0078`, cho thấy phần tìm khung người không cải thiện sau fine-tune.

2. Sau fine-tune, `box_mAP50-95 = 0.8041` và `pose_mAP50-95 = 0.6908`, chênh `0.1133`. Model tìm người dễ hơn tìm khớp: box chỉ cần xác định vùng người, còn pose phải đặt đúng 17 điểm, trong đó có các điểm nhỏ hoặc bị che như tai, mắt và cổ tay.

3. Chưa thể xác định ảnh test và loại lỗi từ các file hiện có. Notebook có cell dự đoán 10 ảnh test, nhưng workspace chưa có thư mục predictions hoặc ảnh kết quả để đối chiếu trực quan; không đủ bằng chứng để gọi là lệch nhẹ, đảo trái/phải, nhầm người hay trượt hẳn.

4. Chưa có bảng `OKS model vs nhãn của bạn` được lưu từ cell 6 của notebook, nên chưa thể xác định ảnh thấp nhất hoặc kết luận ai đúng. Cần chạy cell đối chiếu rồi xem ảnh gốc cùng pose của bạn và pose model dự đoán.

5. Kết quả gold cho biết trước rework, ca thấp nhất trong ba skeleton cần sửa là `train_01.jpg`, người #2, OKS `0.855`; nhưng chưa có bảng OKS model-vs-nhãn nên chưa thể biết đây có phải ảnh model đoán tệ nhất hay không. Vì vậy chưa thể kết luận ảnh đó khó với cả người gán và model chỉ từ kết quả gold.

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

Ở ảnh `train_07`, người thứ 1, tôi chọn `right_ankle` là `v=0`. Phần cẳng chân đi xuống sát mép dưới ảnh nhưng bàn chân và vị trí cổ chân đã nằm ngoài khung, nên không còn bề mặt hoặc phần cơ thể liền kề đủ để đặt chấm chính xác. Đây là khớp thực sự ra ngoài mép ảnh chứ không phải bị vật che trong khung, vì vậy tôi không đặt chấm và dùng `v=0`.

<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->

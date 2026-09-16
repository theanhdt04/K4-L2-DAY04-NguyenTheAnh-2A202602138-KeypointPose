# Mini guideline - nhóm: **solo** | người gán: **Nguyễn Thế Anh** | ngày: **16/09/2026**

> Điền file này **trong lúc** gán nhãn, không phải sau khi xong. Mỗi lần bạn dừng lại
> hơn 10 giây để phân vân, đó là một dòng phải ghi vào đây.

## 1. Luật bắt buộc (đã thống nhất cả lớp - không sửa)

- Bộ 17 điểm COCO, đúng tên, đúng thứ tự. Lấy từ file `.SVG` chung.
- Mọi người trong ảnh đều có **đủ 17 điểm**. Điểm không dùng được thì gắn cờ, không xoá.
- Trái/phải tính theo **cơ thể người**, không theo bức ảnh.
- Bị che, còn trong khung -> `v = 1`, **vẫn đặt chấm** ở vị trí ước lượng.
- Ra ngoài mép ảnh -> `v = 0`, **không** đặt chấm.
- Không dùng `Hidden` (`h`) - nó không được lưu vào file.

## 2. Luật của nhóm bạn (phải điền)

| Tình huống                                        | Luật nhóm bạn chọn                                                                                                                                   | Vì sao                                                                                                     | Ảnh mẫu từ CVAT                                                                                                                                                                         |
| ------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Hông của người mặc quần áo dài                    | Đặt tại vị trí giải phẫu ước lượng ở hai bên xương chậu/đầu trên xương đùi; nếu bị quần áo che nhưng còn trong khung thì vẫn đặt chấm và chọn `v=1`. | Hông thường không có bề mặt xương nhìn thấy; dùng đường eo, thân và hướng đùi để ước lượng nhất quán.      | <img src="reports/screenshot/train_07.png" width="240" alt="Ảnh CVAT train 07 minh họa vị trí hông bị quần áo che"><br>Hông được suy ra từ eo, thân và hướng đùi.                       |
| Tai bị tóc hoặc mũ bảo hiểm che một phần          | Nếu tai còn trong khung nhưng bị tóc hoặc mũ che thì đặt chấm tại vị trí tai ước lượng và chọn `v=1`; chỉ chọn `v=0` khi tai ngoài mép ảnh.          | Phân biệt bị che với ngoài khung; visibility report cho thấy `left_ear` 62% và `right_ear` 52% `v=1`.      | <img src="reports/screenshot/train_04.png" width="240" alt="Ảnh CVAT train 04 minh họa tai bị mũ bảo hiểm che"><br>Tai vẫn được đặt điểm ước lượng dưới mũ.                             |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | Các khớp còn trong ảnh vẫn phải gán đủ; khớp thực sự ngoài mép ảnh chọn `v=0` và không đặt chấm.                                                     | Không suy đoán điểm đã ra ngoài ảnh, nhưng không dùng `v=0` cho điểm chỉ bị che.                           | <img src="reports/screenshot/train_19.png" width="240" alt="Ảnh CVAT train 19 minh họa người ở sát vùng cắt"><br>Chỉ gán các khớp còn trong khung; không suy đoán điểm đã ra ngoài ảnh. |
| Cổ tay nằm sau tay lái / sau thân mình            | Lần theo cẳng tay và bàn tay; nếu cổ tay còn trong khung nhưng bị che thì đặt chấm ước lượng và chọn `v=1`, không chuyển sang người khác.            | Cổ tay dễ bị nhầm người hoặc trượt khỏi khớp; phải giữ liên tục với cẳng tay của đúng người.               | <img src="reports/screenshot/train_04.png" width="240" alt="Ảnh CVAT train 04 minh họa cổ tay sau tay lái"><br>Cổ tay được suy ra theo liên tục cẳng tay-bàn tay.                       |
| Hai người chồng lên nhau                          | Gán xong đủ 17 điểm của một người rồi mới sang người kế tiếp; điểm bị người kia che nhưng còn trong khung vẫn chọn `v=1`.                            | Đường nối kéo sang cơ thể bên cạnh là dấu hiệu `nham_nguoi`; kiểm theo đường viền và phần cơ thể liên tục. | <img src="reports/screenshot/train_01.png" width="240" alt="Ảnh CVAT train 01 minh họa hai người chồng lên nhau"><br>Mỗi skeleton phải bám đúng một cơ thể.                             |
| Người nhỏ đến mức nào thì không gán nữa           | Không bỏ người theo ngưỡng kích thước; mọi người trong 20 ảnh core đều phải có đủ 17 điểm. Nếu khó nhìn, vẫn gán và ghi ca mơ hồ.                    | Bộ ảnh đã được chọn để gán đủ người; bỏ skeleton sẽ làm thiếu người trong dữ liệu.                         | <img src="reports/screenshot/train_19.png" width="240" alt="Ảnh CVAT train 19 minh họa người nhỏ trong ảnh"><br>Người nhỏ vẫn được gán đủ skeleton.                                     |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `train_01.jpg`, người thứ `2`, khớp `right_wrist`

- Mơ hồ ở chỗ nào: Hai người ở gần nhau nên cổ tay phải dễ rơi sang cơ thể bên cạnh.
- Bạn quyết thế nào: Đặt `right_wrist` theo cẳng tay và bàn tay của người thứ 2, không lấy điểm của người thứ 1.
- Vì sao: Trái/phải tính theo cơ thể người và đường nối cổ tay phải phải liên tục với cẳng tay cùng người.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Model học nhầm người, kéo keypoint sang cơ thể bên cạnh.

### Ca 2 - ảnh `train_04.jpg`, người thứ `1`, khớp `left_wrist`

- Mơ hồ ở chỗ nào: Cổ tay bị tay lái/thân che một phần và ở gần tay của người khác.
- Bạn quyết thế nào: Giữ `left_wrist` trên skeleton người thứ 1, suy ra từ cẳng tay và bàn tay; nếu còn trong khung thì chọn `v=1`.
- Vì sao: Khớp bị che không được xoá hoặc chuyển sang người khác.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Model học sai quan hệ cẳng tay-cổ tay và nhầm keypoint giữa hai người.

### Ca 3 - ảnh `train_19.jpg`, người thứ `2`, khớp `right_wrist`

- Mơ hồ ở chỗ nào: Cánh tay và vật đang cầm làm vị trí cổ tay khó tách khỏi vật thể.
- Bạn quyết thế nào: Theo hướng cẳng tay đến bàn tay đang nắm vật, đặt chấm tại khớp cổ tay của người thứ 2.
- Vì sao: Cổ tay còn trong ảnh nên nếu bị che phải chọn `v=1`; không đặt chấm vào nền hoặc vật thể.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Model học cổ tay bị trượt khỏi khớp thật khi gặp tư thế tương tự.

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: Không áp dụng vì tôi làm bài solo, không có bạn cùng nhóm để đối chiếu.
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**: Không áp dụng; tôi đã tự kiểm bằng `visibility_report.py` và `check_pose_labels.py`.
- Luật mới bổ sung vào mục 2 sau khi thống nhất: Khớp còn trong khung nhưng bị che thì đặt chấm ước lượng và chọn `v=1`; chỉ chọn `v=0` khi khớp thực sự ngoài mép ảnh và không đặt chấm.

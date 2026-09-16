# Mini guideline - nhóm: **\_\_** | người gán: Nguyễn Thế Anh | ngày: 16/09/2026

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

| Tình huống                                        | Luật nhóm bạn chọn                                                                                                                                                                                                                                | Vì sao                                                                                                                      |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Hông của người mặc quần áo dài                    | Đặt tại vị trí giải phẫu ước lượng ở hai bên xương chậu/đầu trên xương đùi. Nếu phần hông bị quần áo che nhưng còn trong khung thì vẫn đặt chấm và dùng `v=1`; không xoá khớp. Ảnh mẫu: `dataset/images/train/train_01.jpg`.                      | Hông thường không có bề mặt nhìn thấy rõ dưới quần áo; dùng đường viền thân, eo và hướng đùi để ước lượng nhất quán.        |
| Tai bị tóc hoặc mũ bảo hiểm che một phần          | Nếu tai còn trong khung nhưng bị tóc hoặc mũ che thì đặt chấm ở vị trí tai ước lượng và dùng `v=1`. Chỉ dùng `v=0` khi tai nằm ngoài mép ảnh. Ảnh mẫu: `dataset/images/train/train_04.jpg`.                                                       | Visibility phải phân biệt bị che với ra ngoài khung; report có `%v=1` cao nhất ở `left_ear` 62% và `right_ear` 52%.         |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | Các khớp phía trên còn trong ảnh vẫn phải gán đủ; khớp thực sự nằm ngoài mép ảnh dùng `v=0` và không đặt chấm. Ảnh mẫu: `dataset/images/train/train_19.jpg`.                                                                                      | Không suy đoán điểm đã ra ngoài ảnh, nhưng cũng không gán `v=0` cho điểm bị che hoặc phần thân còn suy ra được trong khung. |
| Cổ tay nằm sau tay lái / sau thân mình            | Cổ tay còn trong khung nhưng bị tay lái hoặc thân che thì vẫn đặt chấm theo vị trí giải phẫu ước lượng và dùng `v=1`; kiểm tra lại theo cẳng tay và bàn tay. Ảnh mẫu: `dataset/images/train/train_04.jpg`.                                        | Cổ tay là vị trí dễ nhầm người hoặc trượt khỏi khớp; làm xong từng người và không kéo điểm sang cơ thể bên cạnh.            |
| Hai người chồng lên nhau                          | Gán xong toàn bộ 17 điểm của một người trước, theo đường viền quần áo và phần cơ thể liên tục; điểm bị người kia che nhưng còn trong ảnh dùng `v=1`. Không dùng điểm của người trước cho người sau. Ảnh mẫu: `dataset/images/train/train_01.jpg`. | Đường nối kéo sang cơ thể bên cạnh là dấu hiệu `nham_nguoi`; đây là lỗi đã phải sửa ở `train_01.jpg` và `train_04.jpg`.     |
| Người nhỏ đến mức nào thì không gán nữa           | Không đặt ngưỡng kích thước để bỏ người: mọi người trong 20 ảnh core đều phải có đủ 17 điểm. Nếu người nhỏ hoặc khó nhìn, vẫn gán và ghi ca mơ hồ; chỉ dùng `v=0` cho khớp thật sự ngoài mép ảnh. Ảnh mẫu: `dataset/images/train/train_19.jpg`.   | Bộ ảnh đã được chọn để mọi người đủ lớn; bỏ cả skeleton sẽ làm thiếu người và phá vỡ contract 29 skeleton/20 ảnh.           |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `train_01.jpg`, người thứ `2`, khớp `right_wrist`

- Mơ hồ ở chỗ nào: Hai người đứng cạnh và cùng cầm đĩa, nên cổ tay phải dễ bị kéo nhầm sang cơ thể bên cạnh.
- Bạn quyết thế nào: Giữ `right_wrist` trên người thứ 2, nối theo cẳng tay của người đó; không lấy điểm của người thứ 1.
- Vì sao: Trái/phải tính theo cơ thể người, và đường nối cổ tay phải phải liên tục với cẳng tay cùng người.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Model học nhầm người, kéo keypoint sang cơ thể bên cạnh khi có nhiều người gần nhau.

### Ca 2 - ảnh `train_04.jpg`, người thứ `1`, khớp `left_wrist`

- Mơ hồ ở chỗ nào: Người lái xe đội mũ bảo hiểm, cổ tay bị tay lái và thân xe che một phần; tay còn lại của người thứ 2 ở gần vùng này.
- Bạn quyết thế nào: Đặt `left_wrist` theo cẳng tay và bàn tay của người thứ 1, giữ trong đúng skeleton của người đó và đánh dấu `v=1` nếu bị che.
- Vì sao: Cổ tay vẫn nằm trong khung và có thể suy ra từ phần cẳng tay liền kề, nên không được xoá hoặc chuyển sang người khác.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Model học quan hệ sai giữa cẳng tay và cổ tay, đồng thời học nhầm keypoint giữa hai người chồng lấn.

### Ca 3 - ảnh `train_19.jpg`, người thứ `2`, khớp `right_wrist`

- Mơ hồ ở chỗ nào: Người thứ 2 đang giữ thanh điều khiển; cánh tay, dây và ván che làm vị trí chính xác của cổ tay khó tách khỏi vật thể.
- Bạn quyết thế nào: Dựa vào hướng cẳng tay đi tới bàn tay đang nắm thanh, đặt chấm ngay tại khớp cổ tay và giữ thuộc người thứ 2.
- Vì sao: Khớp vẫn ở trong ảnh nên dùng `v=1` nếu bị che; không đặt chấm ra ngoài hoặc trượt khỏi vị trí khớp.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Model học cổ tay ở vị trí vật thể hoặc ngoài khớp thật, làm dự đoán bị trượt hẳn khi gặp tư thế tương tự.

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: Chưa xác định được vì repo chưa có bảng `visibility_compare.md` hoặc dữ liệu nhãn của bạn cùng nhóm.
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**: Chưa đủ dữ liệu để kết luận; cần chạy lại `visibility_report.py --compare` với thư mục nhãn của bạn cùng nhóm.
- Luật mới bổ sung vào mục 2 sau khi thống nhất: Khớp bị che nhưng còn trong khung phải đặt chấm ước lượng và chọn `v=1`; chỉ chọn `v=0` khi khớp thực sự nằm ngoài mép ảnh. Với hai người gần nhau, phải lần theo cẳng tay/đùi và đường viền của từng người trước khi đặt điểm, không chuyển điểm sang cơ thể bên cạnh.

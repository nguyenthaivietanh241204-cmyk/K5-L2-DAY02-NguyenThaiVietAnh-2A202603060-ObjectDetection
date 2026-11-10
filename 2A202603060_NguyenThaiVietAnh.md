# Báo cáo cá nhân — Ngày 2 Object Detection

## 1. Thông tin học viên
- Họ tên: Nguyễn Thái Việt Anh
- MSSV: 2A202603060
- Email:nguyenthaivietanh241204@gmail.com   
- Lớp L2A
- Link repo bài làm: https://github.com/nguyenthaivietanh241204-cmyk/K5-L2-DAY02-NguyenThaiVietAnh-2A202603060-ObjectDetection
- Link Colab đã chạy: (https://colab.research.google.com/github/nguyenthaivietanh241204-cmyk/K5-L2-DAY02-NguyenThaiVietAnh-2A202603060-ObjectDetection/blob/main/notebooks/day2_annotation_to_yolo.ipynb)

## 2. Schema và mini guideline
Chi tiết trong [GUIDELINE_MINI.md](GUIDELINE_MINI.md).
- Ba ca mơ hồ đã quyết định: (1) drive_007 ; (2) drive_030 ; (3) drive_041 
- Cách áp dụng schema: mỗi xe một box riêng; box ôm sát phần nhìn thấy; xe bị che hoặc cắt mép vẫn gán nếu nhận ra được lớp; xe đỗ vẫn gán theo loại xe; không gán mô tô/xe máy, người, xe đạp, phản chiếu, hình xe trên bảng quảng cáo.
- Phần cần giảng viên làm rõ:

## 3. Annotation và self-QC
- Số file nhãn train: 50 (đã kiểm tra bằng `ls dataset/labels/train | wc -l` trên Colab, kết quả 50).
- Công cụ: CVAT online, task 50 ảnh, 4 lớp theo thứ tự car, truck, bus, van; xuất định dạng YOLO 1.1.
- Kết quả checker và lỗi đã xử lý: …
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: drive_…, …
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa: …


## 4. Gold QC và rework
| Chỉ số | Trước sửa | Sau sửa nếu có |
|---|---|---|
| TP | 462 | … |
| FP | 883 | … |
| FN | 191 | … |
| Precision | 0.3435 | … |
| Recall | 0.7075 | … |
| F1 | 0.4625 | … |
| mean_iou_of_matches | 0.8123 | … |
| passed | false | … |

Kết quả nằm ở [outputs/annotation_evaluation.json](outputs/annotation_evaluation.json).

Nhận xét từ số liệu: mean IoU đạt (0.81 ≥ 0.70) nên box khít; F1 chưa đạt (0.46 < 0.80). Tôi vẽ 1345 box trong khi gold có 653 box. Ảnh drive_006 có 0 box trong khi gold có 21 box.

Rework: chưa rework tính đến thời điểm nộp báo cáo này. Lý do: … Nguyên nhân của FP/FN chưa được xác định vì tôi chưa mở lại từng ảnh để kiểm tra.
(Nếu bạn đã rework, thay đoạn này bằng: ảnh đã mở lại, lỗi thật sự thấy, quyết định sửa/giữ và lý do.)

## 5. Kết quả YOLO
Chưa train. Theo hướng dẫn, chỉ train sau khi đạt F1 ≥ 0.80 và mean IoU ≥ 0.70; nhãn của tôi chưa đạt ngưỡng nên chưa chạy phần này.

- Runtime, phiên bản Ultralytics và Torch: …
- Tham số thay đổi so với notebook: …
- Đường dẫn best checkpoint: …

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---|
| Precision | … |
| Recall | … |
| mAP50 | … |
| mAP50–95 | … |

Bốn câu hỏi cuối notebook:
1. Lớp recall thấp nhất và ảnh minh họa:
2. mAP50 chỉ cần box dự đoán chồng lên box thật tối thiểu 50%, còn mAP50-95 lấy trung bình ở các ngưỡng IoU từ 0.50 đến 0.95. Nếu mAP50 cao mà mAP50-95 thấp thì model tìm đúng xe nhưng box chưa khít. Trên box cần kiểm tra: box lỏng (chừa nền, xe bên cạnh) hay chặt (cắt mất nóc, bánh), có lệch theo một hướng không, cách vẽ có nhất quán giữa các ảnh không, và xe bị che hoặc cắt mép có theo cùng một quy tắc không.
3. Lỗi class liên quan guideline
4. Train bằng ảnh eval sẽ làm model “thuộc” chính các ảnh đó, nên chỉ số cao giả tạo và không phản ánh khả năng nhận diện ảnh mới (rò rỉ dữ liệu). Đề cũng cấm dùng eval để train. Trong notebook, 10 ảnh này làm validation: theo dõi chỉ số sau mỗi epoch và chọn best.pt. Vì vừa chọn checkpoint vừa báo cáo kết quả nên chúng không phải test set độc lập.

## 6. Khó khăn và cách xử lý
| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| Gán nhãn trên CVAT | Mất nhiều thời gian hơn dự kiến | Dùng phím tắt và làm theo quy tắc guideline | Gán xong 50 ảnh, nhưng nộp sau hạn |
| Upload nhãn lên GitHub | Phải upload nhiều file .txt qua trình duyệt | Dùng Add file → Upload files vào dataset/labels/train | Đủ 50 file |
| Clone repo trên Colab | git clone báo exit status 128 | Phát hiện REPO_URL còn chữ mẫu, sau đó có dấu cách thừa đầu link; đã sửa | Clone thành công |
| Giải nén gold | `unzip` không mở được | Nhận ra file gold là .rar, dùng unrar | Giải nén được 50 file gold |
| Chấm gold | F1 0.46 chưa đạt; drive_006 có 0 box | … | … |

## 7. Tự đánh giá theo rubric
- Đã có kết quả: 50 file nhãn YOLO; GUIDELINE_MINI.md; kết quả chấm gold lần đầu (annotation_evaluation.json, passed = false).
- Còn thiếu hoặc chưa kiểm được: rework đạt ngưỡng F1 và mean IoU; checker và rà 10 ảnh bằng mắt (…); train và đánh giá trên 10 ảnh eval; link Colab; ảnh và vật thể dẫn chứng; hai thư mục assets/eval_predictions/ và assets/yolo26_runs/.
- Tôi không tự nhận hoàn thành các bước chưa chạy.

## 8. Công cụ AI và tài liệu tham khảo
- Công cụ AI: Claude (Anthropic). Dùng để hướng dẫn thao tác CVAT, GitHub, Colab, gỡ lỗi clone và giải nén, đọc kết quả chấm, và soạn nháp báo cáo.
- Phần tự làm và tự kiểm tra: tự gán nhãn 50 ảnh trên CVAT, tự chạy các ô trên Colab, đối chiếu số liệu với outputs/annotation_evaluation.json. (Sửa lại nếu thực tế khác.)
- Nguồn ngoài repo: CVAT (app.cvat.ai), tài liệu Ultralytics.
- Không dùng mật khẩu/token và không đính kèm gold train.
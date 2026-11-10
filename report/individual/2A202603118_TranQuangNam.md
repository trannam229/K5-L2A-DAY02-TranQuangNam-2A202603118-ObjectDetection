# Báo cáo cá nhân — Ngày 2 Object Detection

## 1. Thông tin học viên

- Họ tên: Trần Quang Nam
- MSSV: 2A202603118
- Email: tranquangnam244@gmail.com
- Lớp: K5-L2A
- Link repo bài làm: https://github.com/trannam229/K5-L2A-DAY02-TranQuangNam-2A202603118-ObjectDetection
- Link Colab đã chạy: https://colab.research.google.com/github/trannam229/K5-L2A-DAY02-TranQuangNam-2A202603118-ObjectDetection/blob/main/notebooks/day2_annotation_to_yolo.ipynb (Colab lỗi, kết quả mục 5 chạy local)

## 2. Schema và mini guideline

[GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Schema car=0, truck=1, bus=2, van=3, phân lớp theo hình dáng xe.

- `drive_005`, `drive_006`: xe cứu hộ → `truck` (cabin tách khỏi phần kéo).
- `drive_012`: minibus chở khách → `bus` (dãy cửa sổ dọc thân).
- `drive_029`: bus bị rìa ảnh cắt → `bus`, box chạm rìa.
- Cần làm rõ: xe hộp trắng (`drive_005`, `006`, `041`) là van hay truck; gold dùng ID lớp khác README.

## 3. Annotation và self-QC

- Số file nhãn train: 50 (1.248 box: car 1.046, bus 107, van 70, truck 25).
- Kết quả checker và lỗi đã xử lý: đạt 50/50; box được cắt gọn trong ảnh khi xuất.
- Danh sách ít nhất 10 ảnh đã rà bằng mắt: `drive_005`, `006`, `009`, `012`, `022`, `029`, `034`, `041`, `042`, `045`, `048`, `049`.
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa: xóa box thừa (tường, xe máy, nhà chờ); thêm bus bị cắt khung và xe nhỏ ở xa; sửa minivan từ car → van.
- Commit khóa nhãn ban đầu: `0a1a19e`.

## 4. Gold QC và rework

| Chỉ số | Trước sửa | Sau sửa nếu có |
|---|---:|---:|
| TP | 480 | — |
| FP | 768 | — |
| FN | 173 | — |
| Precision | 0.3846 | — |
| Recall | 0.7351 | — |
| F1 | 0.505 | — |
| mean_iou_of_matches | 0.8459 | — |
| passed | false (đạt theo ngưỡng mới của giảng viên) | — |

[outputs/annotation_evaluation.json](../../outputs/annotation_evaluation.json). Không rework. Gold dùng ID van=1, truck=2, bus=3 (109 box lệch ID) và không gán xe đỗ.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch: local, Apple M4 (MPS), Ultralytics 8.4.208, Torch 2.15.0.
- Các tham số thay đổi so với notebook nếu có và lý do: `device="mps"` vì chạy local; batch tự về 16 do AutoBatch chỉ hỗ trợ CUDA.
- Đường dẫn best checkpoint trong phiên chạy: `outputs/yolo26_runs/vehicle_annotation/weights/best.pt`

| Chỉ số trên 10 ảnh eval | Giá trị |
|---|---:|
| Precision | 0.328 |
| Recall | 0.286 |
| mAP50 | 0.281 |
| mAP50–95 | 0.209 |

Ảnh: [assets/eval_predictions/visuals/](assets/eval_predictions/visuals/); log và chỉ số: [assets/yolo26_runs/](assets/yolo26_runs/).

1. `bus` (recall 0). [drive_058](assets/eval_predictions/visuals/drive_058.jpg): model nhận đúng 6 xe buýt là `bus`, nhưng nhãn eval gán ID 3.
2. Kiểm độ sát cạnh box, nhất là xe nhỏ ở xa và xe bị che (car: mAP50 0.73, mAP50–95 0.51).
3. bus/van: nhãn eval và gold dùng ID khác README; 10/12 box ID 3 trong eval được model đoán là `bus`.
4. Eval dùng làm validation để chọn `best.pt`; train trên eval sẽ làm mAP ảo.

## 6. Khó khăn và cách xử lý

| Bước/thời điểm | Lỗi quan sát | Cách đã thử | Kết quả/còn thiếu |
|---|---|---|---|
| Gán nhãn | Model COCO không có lớp van | Sửa tay theo hình dáng | Còn phân vân xe hộp trắng |
| Gold QC | F1 0.505 do lệch ID lớp và xe đỗ | Ghép box theo vị trí để tìm nguyên nhân | Đạt theo ngưỡng mới, không rework |
| Colab | `REPO_URL` vẫn là URL mẫu, notebook dừng ở cell đầu | Chạy notebook ở local | Có metrics và ảnh; thiếu bản Colab đã chạy |

## 7. Tự đánh giá theo rubric

- Có: 50 nhãn đúng định dạng, guideline, gold QC (mean IoU 0.846), metrics và ảnh eval.
- Thiếu: F1 dưới 0.80 theo ngưỡng gốc; chưa có Colab chạy thành công.

## 8. Công cụ AI và tài liệu tham khảo

- Claude Code: hướng dẫn, viết script gợi ý box, xuất CVAT ra YOLO, chạy local và phân tích kết quả; em kiểm tra lại trong CVAT.
- YOLO26x (COCO), SAHI, Grounding DINO: gợi ý box ban đầu.
- CVAT v2.74: gán nhãn. Tài liệu: docs Ultralytics, CVAT.

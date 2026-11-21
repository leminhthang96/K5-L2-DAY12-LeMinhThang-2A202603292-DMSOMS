# Tự đánh giá — Lê Minh Thắng · G03

**MSHV:** 2A202603292. 

## 1. Tự rà soát 4 cảnh

check_final.txt ghi đủ 22 ảnh, 0 lỗi và 8 cảnh báo. Cảnh báo và bất đồng chưa tự chứng minh nhãn sai.

| Ảnh | Đối tượng | Loại lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|
| S03_ir.png (OMS) | object, rear_right | wrong_class (cần xác minh) | Mine là cup, peer là other. Chưa đủ căn cứ chốt lớp; IR đã mất màu. Xem hình dạng trên CVAT; không chắc thì other (§4.4-4, §4.8). | Chưa; chưa phân xử dòng này. |
| S05_ir.png (OMS) | object, rear_middle | wrong_class (cần xác minh) | Mine là bag, peer là cup; bất đồng cũng có ở RGB. Không coi hai ảnh sáng khác nhau là bằng chứng về loại vật. Kiểm tra riêng từng ảnh (§4.8). | Chưa; chưa phân xử dòng này. |
| D01.png (DMS) | face và điểm mắt face13 | flag (cảnh báo cần xét) | Hai mắt của mine là unknown, peer là open; log ghi ambiguous. Các điểm mắt mine đều không bật occluded/outside. Cần đối chiếu trạng thái mắt và từng điểm trên CVAT (§4.5–4.6). | Chưa; tạm giữ unknown theo log. |
| D03.png (DMS) | Điểm mắt face13 | flag (cảnh báo cần xét) | Mine để occluded=0, peer để 1 ở 8 điểm mắt; cả hai gán hai mắt unknown. Chưa xác minh điểm nào bị che. Định vị chắc điểm bị che thì occluded, không định vị được thì outside (§4.6). | Chưa; chưa kết luận bộ cờ nào đúng. |

## 2. Lỗi mình lặp lại nhiều nhất hôm nay

**Điểm cần rà soát lặp lại:** mắt unknown nhưng các điểm mắt không có cờ occluded/outside. Cảnh báo D01 có từ check_cpB.txt đến check_final.txt; D03, D05 và D06 cũng có cảnh báo liên quan. Chưa đủ bằng chứng gọi tất cả là lỗi thiếu cờ.

**Vì sao mình mắc:** chưa xác định được nguyên nhân thao tác từ log. Cần bổ sung bước kiểm tra đồng thời thuộc tính mắt và các điểm mặt, không chỉ xem số lỗi của script.

**Lần sau tránh bằng cách:** kiểm riêng từng mắt và từng điểm trên CVAT; chỉ gán open/closed khi thấy rõ, dùng cờ theo §4.6 và ghi lý do cho cảnh báo còn lại. Không bật cờ hàng loạt chỉ để hết WARN. Luôn gọi ghế theo xe, trái/phải mắt và tay theo người.

## 3. Ghi chú về disagreement_log

Hiện có 14/64 dòng đã điền đủ ba cột, tất cả là ambiguous; 50 dòng còn trống. Chưa có dòng xác nhận peer đúng và mình sai, nên không nêu một ví dụ như đã phân xử.

Điều học được: hai bản giống hoặc khác nhau đều chưa chứng minh đúng/sai. Ví dụ S01_ir.png, peer dùng occupied=yes không hợp lệ; điều đó chưa đủ chứng minh mine bỏ box là đúng. Mentor đã miễn nhãn trẻ em; ghế trẻ em trống vẫn theo guideline. Các ca chưa rõ cần hỏi mentor, không đoán.

Lượt CP9 chỉ viết báo cáo; chưa sửa nhãn và chưa tạo export_final_v2.zip.

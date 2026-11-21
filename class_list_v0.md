# Danh sách lớp v0 — LeMinhThang · G03

## Căn cứ và phạm vi

Dựa trên GUIDE Cabin v1.0 (§3–4.9), SUBMISSION (E4–E5), RUBRIC, hai export và disagreement_log.csv của G03. Nhãn trong export là kết quả đang review, chưa phải đáp án đúng.

IR_sim là S##_ir của SVIRO; real_IR là D## của Drive&Act. Các số đo trong ir_log.csv được tính ngay trên máy bằng Pillow/NumPy: độ sáng mỗi pixel = (R+G+B)/3, thang 0–255; trung vị tính trên toàn ảnh; bỏ kênh alpha. Chỉ số đo và nhãn được dùng để viết log; chưa xác nhận trực quan mắt, kính hoặc hình dạng vật. Không khẳng định có chói kính, mắt sáng hay suy giảm sáng theo khoảng cách. Không gửi ảnh ra ngoài.

Bảng dùng đúng lớp/thuộc tính hiện có. frame_meta là tag toàn ảnh, không phải box. Phần “nhìn thấy trên IR” nêu điều kiện theo guideline, không khẳng định mọi ảnh G03 đều nhận biết được.

## DMS (10 lớp / thuộc tính)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng DMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person | Box; seat=driver | Xác định vùng tài xế để kiểm tra mặt, tay và dây an toàn. | Có thể dựa vào phần cơ thể thấy được; không suy phần bị che. |
| 2 | face | Box mặt | Khoanh vùng để đọc mắt, kính và hướng nhìn. | Có khi thấy mặt; không vẽ nếu gần hết mặt bị che, không thấy cả mắt lẫn mũi. |
| 3 | face13 | 13 điểm; occluded/outside | Xác định vị trí mắt, mũi, miệng để hỗ trợ phân tích mặt. | Chỉ khi mặt rộng ít nhất 60 px. Điểm che: occluded nếu định vị chắc, outside nếu không định vị được. |
| 4 | hand | whose=driver/passenger; side=left/right; on_wheel=yes/no/unknown | Theo dõi tay và việc chạm vô lăng. | Có nếu thấy bàn tay và chỗ tiếp xúc; chưa rõ thì on_wheel=unknown. |
| 5 | phone | state=held/mounted/lap | Nhận biết điện thoại và cách sử dụng. | Cần thấy cạnh, góc hoặc màn hình; tay gần tai chưa đủ để vẽ phone. |
| 6 | face.eye_left / eye_right | open/closed/unknown | Theo dõi trạng thái từng mắt; chuỗi nhiều khung mới hỗ trợ đánh giá nhắm mắt kéo dài. | Cần thấy khe mắt hoặc mí khép; che hay không phân biệt được thì unknown. |
| 7 | face.glasses | unknown/none/clear/sun | Biết tài xế có đeo kính để xử lý khó khăn khi đọc mắt. | Có thể nhận khung/tròng; kính râm trên NIR có thể trông trong. Không rõ thì unknown. |
| 8 | face.gaze_zone | road/mirror_l/mirror_r/mirror_c/cluster/center/lap/other | Theo dõi vùng chú ý của tài xế. | Dựa vào hướng đầu và mắt; không chắc thì other, ghi lý do. |
| 9 | person.seatbelt | worn_correct/worn_incorrect/not_worn/unknown | Kiểm tra việc đeo dây và đường đi của dây. | Cần thấy rõ dải dây hoặc rõ không có dây; tối, che hay đang thắt dở thì unknown. |
| 10 | frame_meta (tag) | modality=ir; light=day/night/unknown; camera_blocked=yes/no | Ghi loại ảnh và tình trạng camera để hiểu kết quả DMS. | D## là NIR thật; ảnh xám hoặc tối không tự xác nhận ban đêm. |

Trên D## không xoay ảnh: trái/phải theo người, mắt trái có y lớn hơn mắt phải. Không gán object cho chai, cốc hoặc kính trên tay. Một khung mắt closed chưa đủ kết luận buồn ngủ.

## OMS (6 lớp / tag)

| # | Lớp / thuộc tính | Giá trị | Để làm gì (chức năng OMS) | Nhìn thấy được trên IR? |
|---|---|---|---|---|
| 1 | person | Box người lớn; seat theo xe; seatbelt | Biết ghế nào có người lớn và kiểm tra dây khi thấy được. | Có thể nhận dáng người; bị che vẫn ôm phần thấy được. SVIRO chỉ dùng seatbelt=not_worn/unknown. |
| 2 | face | Chỉ box mặt người lớn | Bổ sung vùng mặt cho người trên ghế. | Có nếu thấy mặt; OMS không gán thuộc tính mắt và không vẽ face13. |
| 3 | child_seat | Box; seat; occupied=no/unknown | Phân biệt ghế trẻ em trống với đồ vật hay ghế xe thông thường. | Dựa vào hình dạng; bên trong không rõ thì unknown. Cấm occupied=yes. |
| 4 | infant_seat | Box; seat; facing=rear/front | Nhận biết nôi xách trống và hướng đặt. | Có thể dựa vào hình dạng, hướng ghế; ca không rõ cần hỏi mentor, không tự thêm giá trị thuộc tính. |
| 5 | object | Box; seat; type=bag/box/cup/other | Biết ghế nào có đồ và loại đồ mang theo. | IR mất màu nên dựa vào hình dạng, vị trí; chưa chắc loại thì other. |
| 6 | frame_meta (tag) | modality=rgb/ir; light=unknown; camera_blocked=yes/no | Tách RGB với IR-sim và ghi tình trạng camera. | S##_ir là IR mô phỏng; không dùng để khẳng định hiện tượng quang học của NIR thật. |

Ghế theo xe: bên trái ảnh là rear_right. Ghế xe trống không vẽ box. Vật trong ghế trẻ em có box object riêng, cùng seat với child_seat. Mentor đã xác nhận không cần gán nhãn trẻ em; ghế trẻ em trống vẫn theo guideline.

## 2 câu hỏi leo thang

1. **Câu hỏi:** Mentor có thể chỉ mẫu thế nào là đủ rõ để chốt open, và khi mắt còn unknown thì từng điểm mắt cần cờ gì? Cần phân biệt mức thấy trạng thái mắt với mức định vị được mép mí.
   **Khung ví dụ:** G03 D01.png: mine gán hai mắt unknown, peer gán open; các điểm mắt của mine đều có occluded=0 và outside=0. Log đang ambiguous.
   **Tạm gán:** Giữ eye_left/eye_right=unknown theo log; chưa đổi cờ chỉ vì cảnh báo script. Khi xem trên CVAT, điểm bị che chỉ dùng occluded nếu định vị chắc; không định vị được thì outside (§4.5–4.6). Cần mentor xác nhận từng điểm.

2. **Câu hỏi:** Với vùng nghi có trẻ em đã được miễn gán, mentor muốn bỏ cả vùng hay vẫn giữ box ghế khi còn nhận ra ghế? Cần làm rõ phạm vi ngoại lệ so với quy tắc gán ghế trống.
   **Khung ví dụ:** G03 S01_ir.png, ghế rear_right: mine không có child_seat; peer có child_seat với occupied=yes. Export không đủ chứng minh ghế trống; log đang ambiguous.
   **Tạm gán:** Chưa thêm box, chưa gán nhãn trẻ em; không dùng occupied=yes. Nhờ mentor xem trên CVAT local. Nếu xác nhận ghế trống thì child_seat, occupied=no; nếu xác nhận là ghế nhưng bên trong không rõ thì unknown (§4.1, §4.8). Đây là quyết định tạm chờ xác nhận.

Các cách tạm gán là hướng xử lý khi review; CP8 chỉ tạo hai file này, chưa sửa nhãn trong export.

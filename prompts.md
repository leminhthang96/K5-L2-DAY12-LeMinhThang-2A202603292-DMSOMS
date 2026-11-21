# Khai báo dùng AI — Lê Minh Thắng

**MSHV:** 2A202603292 · **Bộ ảnh:** G03.

## Các lượt dùng Codex đã xác nhận

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | Codex | Đọc guideline và hai export; điền ít nhất 5 dòng disagreement, không đoán và không sửa nhãn. | Codex điền đủ ba cột cho 14/64 dòng, tất cả ambiguous, kèm lý do và quy tắc. | Codex đối chiếu XML, kiểm UTF-8, các cột khác và mã băm script/export. Chưa xác nhận trực quan trên CVAT. |
| 2 | Codex | Hoàn thành CP8: ir_log.csv và class_list_v0.md dựa trên G03. | Tạo 4 quan sát (2 IR_sim, 2 real_IR), 10 mục DMS, 6 mục OMS và 2 câu hỏi mentor. Có dùng mã do AI viết để đo số liệu ảnh ngay trên máy. | Codex kiểm số đo bằng Pillow/NumPy, cấu trúc CSV, số mục, UTF-8 và việc giữ nguyên các file cũ. Không coi số đo là bằng chứng trực quan về mắt hay vật. |
| 3 | Codex | Hoàn thành CP9 theo mẫu, dùng kết quả thật; hỏi thông tin người review còn thiếu. | Soạn self_review.md, exit_ticket.md, TEAM.md và file khai báo này; có hỗ trợ trả lời exit ticket. | Đối chiếu GUIDE, SUBMISSION, mẫu, XML và log; kiểm số liệu, phép tính thời gian và tính toàn vẹn file. Việc học viên tự kiểm thủ công chưa được xác nhận. |

## ChatGPT ngoài cuộc chat Codex này

**Chờ Lê Minh Thắng xác nhận:** đã dùng ChatGPT riêng cho việc gì, câu hỏi chính và cách dùng kết quả. Chưa có lịch sử được cung cấp nên chưa thể ghi “đã dùng” hoặc “không dùng”.

## Dữ liệu và giới hạn

- Trong các lượt Codex trên, ảnh gốc và ảnh chụp màn hình cabin không được gửi vào mô hình hoặc dịch vụ ngoài. CP8 chỉ chạy tính toán ảnh cục bộ rồi đọc số đo và nhãn.
- Codex có hỗ trợ review dữ liệu nhãn và soạn báo cáo; không tự vẽ hay sửa nhãn trong export, không sửa script kiểm tra.
- Các bất đồng còn thiếu bằng chứng được giữ chờ xác nhận. Chưa có bằng chứng mentor đã phân xử hoặc học viên đã kiểm lại toàn bộ kết quả AI.

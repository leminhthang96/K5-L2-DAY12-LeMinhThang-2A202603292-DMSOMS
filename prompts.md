# Khai báo dùng AI — Lê Minh Thắng

**MSHV:** 2A202603292 · **Bộ ảnh:** G03.

Tôi có sử dụng **ChatGPT và Codex** trong bài lab. Các yêu cầu dưới đây được tóm tắt, không phải nguyên văn prompt.

| # | Công cụ | Bạn hỏi gì (tóm tắt) | Bạn dùng kết quả thế nào | Bạn có kiểm lại không? Bằng gì? |
|---|---|---|---|---|
| 1 | ChatGPT | Phân tích và giải thích guideline của bài lab Day12 DMS-OMS. | Tôi dùng phần giải thích để hiểu quy tắc rõ hơn, hạn chế nhầm lẫn và giảm lỗi khi gán nhãn. | Cần đối chiếu với GUIDE.md khi áp dụng; chưa ghi nhận việc kiểm lại từng câu trả lời. |
| 2 | Codex | Đọc hướng dẫn và hai export, hỗ trợ xử lý disagreement_log.csv dựa trên bằng chứng. | Điền đủ ba cột cho 14/64 dòng; tất cả là ambiguous, có mục guideline và lý do bằng tiếng Việt. | Codex đối chiếu XML, kiểm UTF-8 và giữ nguyên các cột khác. Chưa xác nhận trực quan trên CVAT. |
| 3 | Codex | Hỗ trợ CP8: viết ir_log.csv và class_list_v0.md theo mẫu. | Tạo 4 quan sát từ số đo ảnh cục bộ và nhãn; viết 10 mục DMS, 6 mục OMS và 2 câu hỏi mentor. | Codex kiểm số đo bằng Pillow/NumPy, cấu trúc file và số mục. Các số đo không thay cho việc nhìn ảnh để xác nhận mắt hoặc loại vật. |
| 4 | Codex | Hỗ trợ CP9 và viết lại khai báo sử dụng AI. | Soạn self_review.md, exit_ticket.md, TEAM.md và prompts.md; có hỗ trợ trả lời câu hỏi exit ticket. | Codex đối chiếu hướng dẫn, mẫu, XML và log; kiểm phép tính và định dạng file. Việc tôi tự kiểm thủ công toàn bộ nội dung chưa được xác nhận. |

## Dữ liệu và giới hạn

- Trong các lượt Codex trên, không gửi ảnh gốc hoặc ảnh chụp màn hình cabin vào mô hình hay dịch vụ ngoài. CP8 chỉ tính toán ảnh trên máy rồi đọc số đo và nhãn.
- Codex hỗ trợ review dữ liệu nhãn và viết báo cáo; không vẽ hoặc sửa nhãn trong export, không sửa script kiểm tra.
- Kết quả AI là phần hỗ trợ. Ca thiếu bằng chứng vẫn cần xem lại trên CVAT hoặc hỏi mentor, không tự coi nhãn của AI hay peer là đáp án đúng.

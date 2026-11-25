# CLAUDE.md: brain tổng

Bộ nhớ chung cho mọi phiên Claude: nghề nghiệp, học tập, dự án, người liên hệ. Mọi kiến thức nằm trong `wiki/`. **Luôn đọc trước, luôn ghi sau.**

## Đọc
Đầu phiên: `wiki/overview.md`, `wiki/hot.md`, khoảng 100 dòng đầu `wiki/nhat-ky.md`, `wiki/index.md`. Rồi đọc note liên quan tới việc đang làm (tìm trong `index.md` hoặc grep `wiki/`). Đã có câu trả lời trong vault thì không hỏi lại.

Dự án có vault riêng thì vào đó làm việc chi tiết; brain tổng chỉ giữ tóm tắt và đường dẫn (xem `wiki/concepts/vi-tri-du-an-va-vault.md`). Nối dự án mới bằng skill `/brain`.

## Ghi (chủ động, không chờ nhắc, viết ngắn)
- Ghi khi có: quyết định, số liệu, hạn chót, kết quả ứng tuyển, đổi kế hoạch, người mới.
- Người, công ty: `wiki/entities/`. Chủ đề, kế hoạch, dự án: `wiki/concepts/`. Tên file kebab-case, tiếng Việt không dấu; có note rồi thì sửa note đó.
- Frontmatter: `type`, `title`, `status`, `created`, `updated`, `tags`. Nối note bằng `[[ten-file]]`.
- Sau mỗi lần ghi: note mới thì thêm vào `index.md`; cập nhật `hot.md`; thêm mục lên đầu `log.md`; thêm một dòng `- **Mảng:** câu` vào mục `## DD/MM/YYYY` hôm nay trong `nhat-ky.md` (giờ Việt Nam; chỉ thêm, không sửa ngày cũ).
- Thông tin nhạy cảm hoặc chưa chắc: hỏi trước khi ghi.

## Luật
- Tiếng Việt, ngắn. Từ nước ngoài dịch nghĩa trong ngoặc ở lần đầu.
- Không ghi mật khẩu, khóa API, cookie, mã xác minh, số giấy tờ vào vault.
- Chỉ ghi điều kiểm được; đoán thì ghi "chưa kiểm". Code hoặc vault riêng của dự án đúng hơn note tóm tắt ở đây; thấy lệch thì sửa note.
- Commit khi user bảo, rồi push lên repo **riêng tư** (`git push`). Commit chỉ lưu trên máy; push mới có bản sao lưu.

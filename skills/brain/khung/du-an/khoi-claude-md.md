## Knowledge Base (vault dự án)

Vault dự án: `{{VAULT}}` (Obsidian, markdown thường). Brain tổng: `{{BRAIN}}`, biết dự án này qua note `wiki/concepts/{{TEN_NOTE}}.md`.

**Đầu phiên:** đọc `vault/wiki/overview.md`, `vault/wiki/hot.md`, khoảng 50 dòng đầu `vault/wiki/nhat-ky.md`, `vault/wiki/index.md`. Đã có câu trả lời trong vault thì không hỏi lại.

**Ghi chủ động, không chờ nhắc:** mỗi khi user viết ra thông tin quan trọng (quyết định, số liệu tài chính, thông tin công ty/pháp lý, ghi chú cuộc họp, hạn chót, liên hệ đối tác, thay đổi kế hoạch, con số hay kết luận đã tính), ghi hoặc cập nhật vào vault ngay trong lúc trò chuyện. Chủ đề đã có note thì sửa note đó, không tạo file trùng.

**Format:**
- Công ty, người, tổ chức: `vault/wiki/entities/<ten-file>.md`. Chủ đề, khái niệm, kế hoạch: `vault/wiki/concepts/<ten-file>.md`.
- Tên file kebab-case, tiếng Việt không dấu.
- Frontmatter: `type` (entity/concept), `title`, `status: developing`, `created`, `updated`, `tags`.
- Tiếng Việt; từ nước ngoài dịch nghĩa trong ngoặc ở lần đầu. Nối note bằng `[[ten-file]]` (không có `.md`).

**Sau mỗi lần ghi:**
- `vault/wiki/index.md`: thêm dòng nếu có note mới.
- `vault/wiki/hot.md`: cập nhật bối cảnh gần đây.
- `vault/wiki/log.md`: thêm mục mới nhất lên đầu.
- `vault/wiki/nhat-ky.md`: thêm một dòng `- **Mảng:** câu` vào mục `## DD/MM/YYYY` của hôm nay (giờ Việt Nam), viết dễ hiểu cho người không đọc code. Chỉ thêm, không sửa hay xóa ngày cũ. Nếu file chưa có trên máy, lấy bản mới nhất trên kho mã trước khi ghi.
- Dự án là repo git: commit phần vault (`git add vault`) tách khỏi code.

**Báo brain tổng** chỉ khi có hạn chót mới hoặc đổi hạn, trạng thái lớn thay đổi (bắt đầu, nộp, có kết quả, dừng), hoặc có người liên hệ quan trọng mới. Khi đó sửa `{{BRAIN}}/wiki/concepts/{{TEN_NOTE}}.md`, rồi `hot.md` và `nhat-ky.md` của brain tổng theo `{{BRAIN}}/CLAUDE.md`. Việc nhỏ chỉ ghi ở vault dự án.

**Không ghi** mật khẩu, khóa API, cookie, mã xác minh, số giấy tờ. Thông tin nhạy cảm hoặc không chắc có nên lưu không: hỏi user trước.

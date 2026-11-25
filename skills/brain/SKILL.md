---
name: brain
description: Brain tổng (second brain) cho mọi dự án. Dùng khi user gõ /brain hoặc nói "nối brain", "nối vào brain tổng", "đăng ký dự án với brain", "tạo vault cho dự án này", "cài brain". Lần đầu trên máy: tạo brain tổng (hoặc clone brain có sẵn). Mỗi dự án: tạo vault riêng, viết CLAUDE.md của dự án, gieo thông tin quan trọng đã có, đăng ký dự án vào brain tổng và đề nghị sao lưu bằng git.
---

# Brain tổng và vault dự án

**Brain tổng** là một vault Obsidian (thư mục markdown thường) có `CLAUDE.md` ở gốc. Nó chỉ cần **biết** từng dự án: dự án ở đâu, là gì, hạn chót, trạng thái. Chi tiết nằm ở vault riêng của dự án (`<dự án>/vault/`). Không gom vault dự án về brain tổng, không chuyển vault đã có đi chỗ khác.

Mẫu file nằm trong thư mục `khung/` cạnh file này (thư mục gốc của skill được báo lúc skill chạy):
- `khung/brain-tong/`: khung brain tổng.
- `khung/du-an/vault/`: khung vault dự án.
- `khung/du-an/khoi-claude-md.md`: khối chèn vào `CLAUDE.md` của dự án.

Chép mẫu (kể cả file ẩn như `.gitignore`, `.gitattributes`, `.gitkeep`) rồi thay các chỗ giữ chỗ:

| Chỗ giữ chỗ | Giá trị |
|---|---|
| `{{NGAY}}` | ngày hôm nay, YYYY-MM-DD |
| `{{NGAY_VN}}` | ngày hôm nay, DD/MM/YYYY |
| `{{BRAIN}}` | đường dẫn tuyệt đối brain tổng |
| `{{TEN_NGUOI_DUNG}}` | tên user trả lời ở bước 2 |
| `{{TEN_DU_AN}}` | tên dự án: tiêu đề README, hoặc câu trả lời của user, hoặc tên thư mục |
| `{{TEN_NOTE}}` | tên note của dự án trong brain tổng, không có `.md` (bước 3) |
| `{{MO_TA}}` | dự án là gì, hạn chót, làm cho ai (bước 4) |
| `{{VAULT}}` | đường dẫn tuyệt đối vault dự án |

Xong thì grep `{{` trong các file vừa tạo, **trừ thư mục `he-thong/`** (bản sao skill, cố ý giữ chỗ giữ chỗ). Phải không còn kết quả.

Dùng `/` trong mọi đường dẫn ghi vào file, để chạy được trên cả Windows, macOS và Linux. Ngày giờ theo giờ Việt Nam (UTC+7). Viết tiếng Việt, ngắn; từ nước ngoài dịch nghĩa trong ngoặc ở lần đầu.

## 1. Tìm brain tổng
Đọc `~/.claude/brain.json`, dạng `{"duong_dan": "<đường dẫn tuyệt đối>"}`. Nếu file có, thư mục tồn tại và có `CLAUDE.md` thì gọi đó là `<brain>` rồi sang bước 3. Nếu không thì làm bước 2.

## 2. Lần đầu trên máy: dựng brain tổng
Hỏi user, gộp vào một tin nhắn:
- Máy này chưa có brain tổng. Bạn đã có brain tổng chưa (một thư mục trên máy, hoặc link repo GitHub riêng tư)?
- Nếu chưa, mình tạo mới ở `~/Brain`. Bạn muốn đặt ở chỗ khác không?
- Tên bạn là gì, để ghi vào brain?

Rồi làm theo câu trả lời:
- **Đã có thư mục trên máy:** kiểm tra có `CLAUDE.md` và `wiki/`. Đúng thì dùng thư mục đó.
- **Đã có repo:** chạy `gh repo view <chủ>/<tên> --json visibility`; repo PUBLIC thì báo user và hỏi lại trước khi dùng. Clone bằng `gh repo clone <chủ>/<tên> <đường dẫn>`, rồi kiểm tra có `CLAUDE.md` và `wiki/`.
- **Tạo mới:** chép `khung/brain-tong/` vào `<đường dẫn>` rồi thay chỗ giữ chỗ. Chép cả thư mục skill này (`SKILL.md` và `khung/`) vào `<brain>/he-thong/skills/brain/` để skill được sao lưu cùng brain. Chưa commit ở đây; git làm một lần ở bước 8.

Tạo `~/.claude/` nếu chưa có, rồi ghi `~/.claude/brain.json` với đường dẫn tuyệt đối (trên Windows viết `\\` hoặc `/` trong JSON).

**Dừng ở đây** nếu thư mục đang mở là chính brain tổng, thư mục nhà, gốc ổ đĩa, hoặc một thư mục trống. Khi dừng, vẫn làm bước 8 cho brain tổng vừa tạo, rồi báo user: "Brain tổng đã sẵn sàng. Vào thư mục dự án nào thì gõ `/brain` để nối dự án đó." Còn lại thì làm tiếp bước 3.

## 3. Xác định dự án
- Gốc dự án là gốc repo git nếu có, không thì là thư mục làm việc hiện tại.
- Đọc `<brain>/CLAUDE.md`, `<brain>/wiki/hot.md`, `<brain>/wiki/index.md`, `<brain>/wiki/concepts/vi-tri-du-an-va-vault.md`.
- Grep `<brain>/wiki` theo tên thư mục và tên dự án để xem brain tổng đã có note về dự án chưa. **Có rồi thì dùng đúng tên note đó**, không tạo note trùng.
- Chưa có thì đặt `{{TEN_NOTE}}` là `du-an-<slug>`. Slug là `{{TEN_DU_AN}}` viết kebab-case, tiếng Việt không dấu. Không lặp tiền tố: thư mục `du-an-demo` cho `du-an-demo`, không phải `du-an-du-an-demo`.
- Xem dự án đã có vault chưa: thư mục `vault/wiki/` ở gốc, đường dẫn trong bảng vị trí, hoặc `CLAUDE.md` của dự án nhắc tới vault. Đã có thì bỏ qua bước 5.

## 4. Chỉ hỏi những gì chưa biết
Đọc trước file có sẵn của dự án (README, CLAUDE.md, notes, reports, tên thư mục) và note trong brain tổng. Chỉ hỏi những gì cả hai chưa trả lời, tối đa 3 câu, gộp vào một tin nhắn:
- Dự án này là gì, trong một câu?
- Hạn chót gần nhất?
- Làm cho ai (cá nhân, nhóm, khách hàng, cuộc thi)?

User không biết thì ghi "chưa rõ", không đoán.

## 5. Tạo vault dự án (nếu chưa có)
Chép `khung/du-an/vault/` vào `<gốc>/vault/` rồi thay chỗ giữ chỗ. `vault/.gitignore` đã lo phần Obsidian bên trong vault.

Mọi note mới về sau bắt đầu bằng frontmatter:
```yaml
---
type: entity        # entity hoặc concept; meta/overview chỉ cho file điều phối có sẵn
title: <tiêu đề có dấu>
status: developing  # developing | evergreen
created: YYYY-MM-DD
updated: YYYY-MM-DD
tags: [...]
---
```

## 6. Viết CLAUDE.md của dự án
Lấy `khung/du-an/khoi-claude-md.md` rồi thay chỗ giữ chỗ.
- Chưa có `CLAUDE.md` ở gốc: tạo mới, chỉ chứa khối này.
- Đã có: **thêm** khối này vào cuối, không sửa hay xóa nội dung cũ. Nếu đã có mục nói về vault, chỉ thêm đoạn "Báo brain tổng" và dòng đường dẫn brain tổng.
- Dự án có quy tắc riêng quan trọng (ví dụ cuộc thi cấm bịa số liệu) thì thêm một dòng cuối khối.

## 7. Gieo nội dung và đăng ký vào brain tổng
**Vault dự án:** đọc lại **toàn bộ cuộc trò chuyện hiện tại** và các file có sẵn của dự án. Ghi mọi thông tin quan trọng chưa có (quyết định, số liệu, hạn chót, liên hệ, kết luận đã tính) theo quy ước trong khối CLAUDE.md.
- Thông tin chung (là gì, hạn chót, file quan trọng ở đâu): `overview.md`. Việc đang mở, hạn gần: `hot.md`.
- Một chủ đề có từ vài ý trở lên (nghiên cứu, thiết kế, kế hoạch, ngân sách): note riêng trong `concepts/`. Người, nhóm, công ty, khách hàng có tên: note riêng trong `entities/`. Thêm note mới vào `index.md`.
- File dài (báo cáo, ghi chú nghiên cứu): tóm tắt kết luận chính và ghi đường dẫn tới file gốc, không chép nguyên văn.
- Chỉ ghi điều kiểm được. Số ước tính hoặc chưa kiểm thì ghi rõ "chưa kiểm".
- Nhạy cảm hoặc không chắc: hỏi trước khi ghi.

**Brain tổng**, làm theo `<brain>/CLAUDE.md`:
- `wiki/concepts/vi-tri-du-an-va-vault.md`: thêm hoặc sửa dòng của dự án (code, vault, repo sao lưu; chưa có repo thì ghi "chưa có").
- `wiki/concepts/{{TEN_NOTE}}.md`: tạo note tóm tắt ngắn (là gì, hạn chót, trạng thái, vault dự án ở đâu), hoặc thêm dòng "Vault dự án: `<đường dẫn>`" vào note sẵn có. Chi tiết để ở vault dự án.
- `wiki/index.md`: thêm vào mục Dự án nếu note mới.
- `wiki/hot.md`: thêm hạn chót nếu có.
- `wiki/log.md`: mục mới lên đầu.
- `wiki/nhat-ky.md`: một dòng vào mục hôm nay.

## 8. Commit và sao lưu
Commit chỉ lưu trên máy; phải push lên repo ngoài máy thì mới có bản sao lưu. Nói rõ điều này với user.

Làm cho từng repo cần lo: **dự án** (nếu vừa nối) và **brain tổng** (nếu vừa tạo mới ở bước 2). Hỏi một lần cho cả hai, gộp vào một tin nhắn.

**Đã là repo git:** commit riêng `vault/` và `CLAUDE.md`, message kiểu `vault: nối dự án vào brain tổng`. Không push, trừ khi `CLAUDE.md` của dự án hoặc user bảo. Repo chưa có remote thì báo user là chưa có bản sao ngoài máy, và đề nghị làm từ mục 5 bên dưới.

**Chưa có git:** đừng tự tạo. Hỏi: "Chưa có git nên chưa được sao lưu. Bạn chọn: (a) git và repo GitHub riêng tư, (b) chỉ git trên máy, hay (c) để sau?" Nếu chọn (a) hoặc (b):
1. `git init` ở gốc.
2. Với dự án, viết `.gitignore` ở gốc nếu chưa có, tối thiểu gồm: `.env`, `.env.*`, `*.pem`, `*.key`, `*cookie*`, `node_modules/`, `.venv/`, `venv/`, `__pycache__/`, `*.db`, `*.sqlite*`, `.cache/`, `dist/`, `build/`. Thêm những thứ khác theo loại dự án. Brain tổng đã có `.gitignore` từ khung.
3. Trước commit đầu: liệt kê file sẽ vào repo (`git add -A --dry-run`), quét chuỗi giống khóa API, mật khẩu, cookie, và tìm file trên 50 MB. Có thì loại ra và báo user, không commit.
4. Commit đầu, gộp cả code và vault, message kiểu `Khởi tạo, nối dự án vào brain tổng` (với brain tổng: `Tạo brain tổng`). Các lần sau mới commit vault tách khỏi code.
5. Chỉ với (a): hỏi tên repo (mặc định là tên thư mục) và tài khoản GitHub. `gh auth status` cho biết tài khoản đang đăng nhập; chưa đăng nhập thì nhờ user tự chạy `gh auth login`. Tạo **riêng tư**: `gh repo create <tài-khoản>/<tên> --private --source=. --remote=origin --push`.
   - User đưa URL repo có sẵn: chạy `gh repo view <chủ>/<tên> --json visibility` trước. **Repo PUBLIC thì dừng, báo user và không push**, vì vault chứa thông tin cá nhân. Chờ user chuyển repo sang private.
6. Kiểm bằng `git ls-remote origin HEAD`, phải ra đúng commit vừa push. Gặp lỗi "Repository not found" thì thường là git đang đăng nhập bằng tài khoản khác. Khi đó đặt riêng cho repo này `git config --local credential.https://github.com.helper ""`, rồi `git config --local --add credential.https://github.com.helper '!gh auth git-credential'`, và thử lại.
7. Ghi repo vào cột "Repo sao lưu" trong bảng `vi-tri-du-an-va-vault.md` của brain tổng.

**Brain tổng về sau:** lần tạo brain, commit đầu nằm trong lựa chọn ở trên. Sau đó, mỗi lần sửa brain tổng (như đăng ký dự án ở bước 7) thì chỉ commit khi user bảo, theo `<brain>/CLAUDE.md`. Commit xong thì push lên remote của nó (`git -C <brain> push`).

## 9. Báo lại
Vài dòng: vault dự án ở đâu, đã ghi những note gì, brain tổng đã sửa những file nào, cái gì còn chờ user (câu hỏi, git, commit brain tổng).

## Sửa skill
Sửa skill thì chép bản mới vào `<brain>/he-thong/skills/brain/` để bản sao lưu luôn khớp.

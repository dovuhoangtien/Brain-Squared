---
type: meta
title: Hướng dẫn hệ thống vault
status: evergreen
created: {{NGAY}}
updated: {{NGAY}}
tags: [meta]
---

# Hướng dẫn hệ thống vault

Brain tổng là thư mục markdown thường. Mở bằng Obsidian ("Open folder as vault", trỏ vào `{{BRAIN}}`). Claude đọc và ghi trực tiếp theo `CLAUDE.md` ở gốc.

## Cấu trúc
- `wiki/overview.md`: đọc đầu tiên.
- `wiki/hot.md`: việc đang mở, ngắn; xong thì chuyển đi.
- `wiki/index.md`: danh mục mọi note.
- `wiki/log.md`: nhật ký kỹ thuật của vault, mới nhất ở trên.
- `wiki/nhat-ky.md`: nhật ký theo ngày cho người đọc, mỗi dòng `- **Mảng:** câu`.
- `wiki/concepts/`: chủ đề, kế hoạch, dự án (một note một chủ đề).
- `wiki/entities/`: người, công ty.
- `he-thong/skills/brain/`: bản sao lưu skill `/brain`.

## Quan hệ với vault dự án
Mỗi dự án giữ vault riêng ở `<dự án>/vault/`. Brain tổng chỉ cần biết dự án tồn tại: nó ở đâu, là gì, hạn chót, trạng thái ([[vi-tri-du-an-va-vault]]). Không gom vault dự án về đây.

Phiên làm việc ở dự án chỉ báo brain tổng khi có hạn chót mới, trạng thái lớn thay đổi hoặc người liên hệ quan trọng mới. Việc nhỏ chỉ ghi ở vault dự án.

## Skill `/brain`
Mở Claude ở thư mục dự án, gõ `/brain` hoặc nói "nối brain". Skill tạo vault dự án, viết `CLAUDE.md` của dự án, gieo thông tin đã có, đăng ký dự án vào đây và đề nghị sao lưu bằng git.

Vị trí brain tổng lưu ở `~/.claude/brain.json`. Máy mới: cài skill `/brain`, gõ `/brain`, trả lời "đã có brain" kèm link repo riêng tư; skill clone về và ghi lại vị trí.

## Sao lưu
Brain tổng là repo git. Commit chỉ lưu trên máy; phải push lên repo GitHub **riêng tư** thì mới có bản sao ngoài máy. `.gitattributes` đặt `merge=union` cho `nhat-ky.md` và `log.md` để nhiều phiên cùng ghi không xung đột.

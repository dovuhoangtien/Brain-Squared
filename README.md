# Brain Squared

Một **brain tổng** (second brain, bộ nhớ thứ hai) cho mọi dự án bạn làm với [Claude Code](https://claude.com/claude-code). Gõ `/brain` một lần ở mỗi dự án là Claude tự:

- tạo vault (sổ ghi chép Obsidian) riêng cho dự án đó,
- viết `CLAUDE.md` để mọi phiên Claude về sau tự đọc và tự ghi vào vault mà không cần nhắc,
- báo cho brain tổng biết dự án tồn tại, nằm ở đâu, hạn chót là gì,
- đề nghị sao lưu bằng git lên repo GitHub riêng tư.

Lần đầu chạy trên máy, nếu chưa có brain tổng, `/brain` tạo luôn (hoặc clone brain có sẵn của bạn từ GitHub về).

```
Brain tổng (~/Brain)                 ← biết mọi dự án tồn tại
├── wiki/concepts/vi-tri-du-an-va-vault.md
├── wiki/concepts/du-an-a.md ──────► D:\Code\du-an-a\vault\   (chi tiết dự án A)
└── wiki/concepts/du-an-b.md ──────► D:\Code\du-an-b\vault\   (chi tiết dự án B)
```

## Cài đặt

**Cách 1: nhờ Claude.** Tải repo này về, mở Claude Code ở bất kỳ đâu và nói:

> Cài skill brain từ thư mục `<đường dẫn tới Brain-Squared>`: chép thư mục `skills/brain` vào `~/.claude/skills/brain`.

**Cách 2: tự chép.**

```bash
git clone https://github.com/dovuhoangtien/Brain-Squared.git
mkdir -p ~/.claude/skills
cp -r Brain-Squared/skills/brain ~/.claude/skills/
```

Mở một phiên Claude Code mới để skill được nạp.

## Dùng

1. Mở Claude Code ở thư mục dự án.
2. Gõ `/brain`, hoặc nói "nối brain".
3. Lần đầu: trả lời brain tổng đặt ở đâu (mặc định `~/Brain`) hoặc đưa link repo brain có sẵn. Những lần sau: chỉ trả lời vài câu về dự án nếu Claude chưa tự đọc ra được.

Mở brain tổng và vault dự án bằng [Obsidian](https://obsidian.md) ("Open folder as vault") để tự xem, tự sửa.

**Máy mới:** cài skill, gõ `/brain`, trả lời "đã có brain" kèm link repo riêng tư của bạn. Claude clone về và nhớ vị trí trong `~/.claude/brain.json`.

## Quy ước

- Viết tiếng Việt; tên file kebab-case không dấu (`du-an-may-tuoi-cay.md`).
- `wiki/entities/`: người, công ty. `wiki/concepts/`: chủ đề, kế hoạch, dự án.
- Bốn file điều phối: `index.md` (mục lục), `hot.md` (việc đang mở), `log.md` (nhật ký kỹ thuật), `nhat-ky.md` (nhật ký theo ngày cho người đọc).
- Muốn đổi quy ước: sửa `skills/brain/SKILL.md` và các file trong `skills/brain/khung/`.

## Quyền riêng tư

Repo này **chỉ chứa hệ thống**, không chứa nội dung của ai. Brain tổng và vault dự án của bạn chứa thông tin cá nhân: chỉ push lên repo **riêng tư**. Skill dừng lại nếu bạn đưa link repo công khai, và không bao giờ ghi mật khẩu, khóa API, cookie hay số giấy tờ vào vault.

## Cấu trúc repo

```
skills/brain/
├── SKILL.md                      # quy trình /brain
└── khung/
    ├── brain-tong/               # khung brain tổng: CLAUDE.md, wiki/
    └── du-an/
        ├── vault/                # khung vault dự án
        └── khoi-claude-md.md     # khối chèn vào CLAUDE.md của dự án
```

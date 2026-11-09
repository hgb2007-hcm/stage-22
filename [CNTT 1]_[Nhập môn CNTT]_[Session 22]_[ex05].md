# Tối ưu quy trình hỗ trợ kỹ thuật nội bộ

Dưới đây là mẫu **Bug Report Template** chuẩn chỉnh và **Quy trình Troubleshooting 3 bước** dành cho nhóm để tối ưu thời gian, tránh làm phiền lẫn nhau vì mấy lỗi vặt môi trường như tràn port hay Docker ngáo.

---

## 1. Mẫu Bug Report Template (Dán vào Notifier/Issue/Group Chat)

Mỗi khi dính lỗi môi trường, thành viên **bắt buộc** phải điền theo form này trước khi tag người khác vào cứu:

```markdown
### 🐛 BUG REPORT: [Tóm tắt lỗi ngắn gọn]

* **1. Context (Bối cảnh):** 
  - Đang làm tính năng/chạy service gì? (vd: Up container DB, chạy local dev)
  - Hệ điều hành & Môi trường: (Windows 11 / WSL2 / macOS M1...)
  - Các bước đã làm trước khi bị lỗi: (vd: Vừa `git pull` nhánh dev về rồi chạy `docker compose up`)

* **2. Expected (Kỳ vọng):**
  - Mong muốn điều gì xảy ra? (vd: Container postgres chạy thành công ở port 5432)

* **3. Actual (Thực tế xảy ra):**
  - Thực tế bị làm sao? (vd: Terminal báo lỗi Bind for 0.0.0.0:5432 failed: port is already allocated)

* **4. Log / Screenshot (Lỗi chi tiết):**
  ```text
  [Dán đoạn Log lỗi dạng TEXT vào đây, KHÔNG chụp ảnh màn hình chữ quá nhỏ trừ khi là giao diện GUI]

```

* Kết quả từ 3 bước tự check (Google/GitHub/AI): (vd: Đã thử kill process trên port 5432 nhưng dịch vụ Postgres service của Win lại tự bật lại)

```

---

## 2. Quy trình 3 bước tra cứu bắt buộc (Self-Troubleshooting Framework)

Trước khi gửi Bug Report vào nhóm, mọi người phải đi qua đủ 3 bước này để tự lọc **80% lỗi vặt**.

```markdown
┌─────────────────┐      ┌──────────────────────────┐      ┌─────────────────────┐
│ 1. Googling     │ ───► │ 2. Community Search      │ ───► │ 3. AI Translation   │
│ (Toán tử chuẩn) │      │ (GitHub Issues / SO)     │      │ (Bóc tách Log lỗi)  │
└─────────────────┘      └──────────────────────────┘      └─────────────────────┘

```

### Bước 1: Googling (Tra cứu từ khóa & Toán tử chuẩn)

* **Cách làm:** Lấy đúng dòng thông báo lỗi chính trong Log (bỏ các thông số riêng như đường dẫn thư mục cá nhân hay IP local).
* **Kỹ thuật:**
* Bọc câu lệnh lỗi trong dấu ngoặc kép: `"port is already allocated" docker`
* Trừ bớt kết quả rác: `-youtube -facebook`



### Bước 2: Community Search (Săn tìm trên GitHub / StackOverflow)

* **Cách làm:** Nếu lỗi liên quan trực tiếp đến một thư viện hay công cụ cụ thể (Docker, Node, Postgres), đi thẳng vào nơi lưu trữ mã nguồn hoặc diễn đàn kỹ thuật.
* **Kỹ thuật:**
* Dùng toán tử tìm Issue: `site:[github.com/docker/for-win/issues](https://github.com/docker/for-win/issues) "bind for 0.0.0.0 failed"`
* Lọc trên StackOverflow: `site:stackoverflow.com "port is already allocated" windows 11`
* *Lưu ý:* Ưu tiên đọc các bình luận có nhiều 👍/❤️ hoặc comment confirm mới nhất (tránh dùng cách fix quá cũ).



### Bước 3: AI Translation (Ép AI bóc tách & Giải thích Log)

* **Cách làm:** Quăng toàn bộ đoạn Log kèm theo file cấu hình liên quan (như `docker-compose.yml`) vào AI để nó dịch ra tiếng người.
* **Prompt mẫu dùng ngay:**
> *"Tôi bị lỗi sau khi chạy Docker: `[Dán Log]`. Hãy giải thích ngắn gọn: (1) Nguyên nhân gốc rễ là gì? (2) Liệt kê 2 cách sửa an toàn nhất theo thứ tự ưu tiên mà không làm ảnh hưởng đến các service khác."*



---

> **Quy định chung của Team:** Nếu sau 3 bước trên (tốn khoảng 10–15 phút) mà vẫn chưa fix được, lúc này mới tạo **Bug Report** theo form trên và quăng vào nhóm để anh em hỗ trợ.
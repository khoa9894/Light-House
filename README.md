# Lighthouse Insights — Kiểm Thử & Đánh Giá Chất Lượng

## Tổng quan

Repo này chứa toàn bộ báo cáo kiểm thử chất lượng của dự án **Lighthouse Insights** — một nền tảng học tập dành cho học sinh tiểu học và phụ huynh. Quá trình kiểm thử được thực hiện theo hai hướng song song: đánh giá hiệu năng/khả năng tiếp cận bằng **Google Lighthouse** và kiểm thử chức năng tự động bằng **Playwright**.

---

## Cấu trúc

```
Admin/              # Lighthouse reports cho 14 trang Admin Panel
Main Web/           # Lighthouse reports cho 12 trang Main Web
sorted_merged.html  # Playwright test report (tổng hợp toàn bộ)
merged.html         # Playwright test report (bản gốc)
```

---

## Kiểm thử hiệu năng — Google Lighthouse

Chạy trên **26 trang** (14 Admin + 12 Main Web), đo 4 chỉ số:

| Chỉ số             | Ý nghĩa                               |
| ------------------ | ------------------------------------- |
| **Performance**    | Tốc độ tải trang, Core Web Vitals     |
| **Accessibility**  | Khả năng sử dụng cho người khuyết tật |
| **Best Practices** | Bảo mật, API chuẩn, HTTPS             |
| **SEO**            | Khả năng index của search engine      |

Mở trực tiếp từng file `.html` trong trình duyệt để xem báo cáo đầy đủ với biểu đồ và chi tiết từng audit.

**Vài con số nổi bật:**

- Performance trung bình toàn hệ thống: **~98/100**
- Best Practices: **100/100** trên gần như tất cả trang
- Trang nhanh nhất (FCP): **0.3s** — Admin/Accounts

---

## Kiểm thử chức năng — Playwright

File test: `arena.spec.ts`  
Chạy trên: Chrome, Edge, Firefox, Safari (WebKit), và project riêng cho Auth flow

**Kết quả: 202/202 passed — 0 failed, 0 flaky**

| Browser  | Tests | Passed |
| -------- | ----- | ------ |
| auth     | 38    | 38     |
| chromium | 51    | 51     |
| edge     | 51    | 51     |
| firefox  | 51    | 51     |
| webkit   | 11    | 11     |

Tổng cộng **89 test cases** bao phủ các luồng chính:

- Đăng nhập / Đăng xuất (bao gồm cả edge case: sai mật khẩu, tài khoản không tồn tại)
- Đăng ký tài khoản học sinh và phụ huynh
- Xem bài học, chủ đề, mốc học tập
- Thi đấu Arena và nộp bài tập
- Lịch sử học tập (lọc theo ngày, loại)
- Bảng xếp hạng, mini-games
- Quên mật khẩu, đổi mật khẩu
- Chỉnh sửa hồ sơ, đổi avatar

Mở `sorted_merged.html` bằng trình duyệt để xem chi tiết từng test, thời gian chạy, và trace.

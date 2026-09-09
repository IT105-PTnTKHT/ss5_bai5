# Thiết kế phân hệ "Yêu cầu Đổi trả & Hoàn tiền (Refund)" — RikkeiShop

Hồ sơ phân tích nghiệp vụ (Lead System Analyst): thiết kế mới hoàn toàn kiến trúc hành vi cho phân hệ Refund, gồm Use Case Diagram tổng thể và Activity Diagram chi tiết cho luồng cốt lõi.

## Cấu trúc repo

```
.
├── BaoCao-Refund-RikkeiShop.docx     # Phần 1: 3 quy tắc nghiệp vụ + 1 Edge case; tóm tắt Phần 2 & 3
├── usecase-diagram-refund.drawio     # Phần 2: Use Case Diagram tổng thể (actors + 10 use case, include/extend)
├── activity-diagram-refund.drawio    # Phần 3: Activity Diagram phân làn cho luồng "Tạo yêu cầu hoàn tiền & thu hồi hàng"
└── README.md
```

## Tóm tắt nội dung

**3 quy tắc nghiệp vụ cốt lõi:**
- BR-01: Chỉ nhận yêu cầu đổi trả trong vòng 7 ngày kể từ khi giao hàng thành công.
- BR-02: Bắt buộc video/ảnh bóc hàng để được duyệt tự động; thiếu bằng chứng → CSKH duyệt thủ công.
- BR-03: RikkeiShop cử Shipper thu hồi hàng tận nhà trong 48h; chỉ giải ngân sau khi QC kho xác nhận hàng đúng tình trạng khai báo.

**Edge case:** Hàng thu hồi bị hư hỏng THÊM do lỗi vận chuyển của Shipper (không phải lỗi gốc của khách) — xử lý bằng cách đối chiếu video bóc hàng gốc, vẫn hoàn tiền đủ cho khách, đồng thời ghi nhận công nợ nội bộ để Shipper bồi thường.

**Use Case Diagram:** 5 tác nhân (Khách hàng, CSKH, Shipper, QC Kho, Payment Gateway), 10 use case với 6 quan hệ `<<include>>` và 3 quan hệ `<<extend>>`.

**Activity Diagram:** phân làn theo 5 tác nhân, thể hiện luồng từ lúc khách tạo yêu cầu đến khi hoàn tất hoàn tiền, bao gồm đầy đủ 3 nhánh rẽ ở bước kiểm định kho (đúng lỗi / hư hỏng do vận chuyển / nghi gian lận).

## Cách mở file sơ đồ

1. Truy cập [app.diagrams.net](https://app.diagrams.net) (draw.io) → File → Open From → Device → chọn file `.drawio` tương ứng.
2. Hoặc mở [Lucidchart](https://lucid.app) → Import → chọn file `.drawio` (Lucidchart hỗ trợ import trực tiếp).

## Hướng dẫn nộp bài (theo quy định đề bài)

1. Tạo repository GitHub mới (public hoặc private + add giảng viên làm collaborator).
2. Push toàn bộ các file trong thư mục này lên repo:
   ```
   git init
   git add .
   git commit -m "Refund subsystem design - RikkeiShop"
   git remote add origin <repo-url>
   git push -u origin main
   ```
3. Copy link repository và nộp lên hệ thống LMS.

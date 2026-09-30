# BÀI TẬP VỀ NHÀ: PHÂN TÍCH RỜI BỎ KHÁCH HÀNG TẠI NETFLIX (BI301 - S02 BTVN VDNC)

---

## 1. Bối Cảnh Bài Toán

Netflix thu tiền định kỳ mỗi tháng từ người dùng thuê bao. Mô hình này có một điểm yếu chí mạng: nếu người dùng hủy gói, dòng tiền mất ngay, không lấy lại được trong tháng đó.

Tình huống đang diễn ra ở thị trường Châu Á, gói Basic:
- Tháng 7: 5 triệu người dùng, 200 nghìn người hủy, CSAT đạt 4.2, giờ xem trung bình 120 giờ/người.
- Tháng 8: 4.95 triệu người dùng, 250 nghìn người hủy, CSAT tụt xuống 3.8, giờ xem còn 110 giờ/người.

Chỉ trong một tháng, số người hủy tăng thêm 50.000 người (+25%). Đây là bài toán cần mổ xẻ thấu đáo trước khi mọi thứ trở nên tệ hơn.

---

## 2. Nhiệm vụ 1: Vẽ Cây Chỉ Số (KPI Tree) 3 Cấp

```
CẤP 1 — [TỔNG DOANH THU THUÊ BAO]
                    |
        +-----------+-----------+
        |                       |
CẤP 2 — [TỔNG USER ACTIVE]   [ARPU — Doanh thu TB/User]
        |                   (Giá gói Basic — cố định)
   +----+----+
   |         |
CẤP 3 — [User Mới]   [User Rời Bỏ — CHURN]
                              |
                      +-------+-------+
                      |               |
               [Churn Rate]    [Nguyên nhân]
               T7: 4.00%            |
               T8: 5.05%       +----+----+
                               |         |
                            [CSAT]   [Giờ Xem TB]
                            4.2→3.8  120→110 giờ
```

Doanh thu Netflix phụ thuộc vào 2 thứ: số người đang dùng và giá gói. Giá gói Basic thường cố định, nên muốn tăng doanh thu phải giữ User Active ở mức cao.

User Active tháng này bằng tháng trước cộng người mới, trừ người hủy. Vấn đề nằm ở nhánh người hủy đang phình ra nhanh. Đào sâu hơn thì thấy CSAT và giờ xem đang đi xuống song song — đây chính là nguyên nhân gốc rễ cần tập trung xử lý.

---

## 3. Nhiệm vụ 2: Phân Tích Nhân Quả — Giờ Xem → CSAT → Churn

Ba chỉ số này không hoạt động riêng lẻ. Chúng kéo nhau đổ xuống theo một trật tự nhất định.

**Giờ xem giảm — tín hiệu đầu tiên cần chú ý**

Tháng 7 mỗi người xem trung bình 120 giờ, tháng 8 còn 110 giờ. Giảm 10 giờ nghe có vẻ nhỏ, nhưng trên gần 5 triệu người thì đó là hàng chục triệu giờ nội dung bị bỏ qua mỗi tháng.

Lý do thường gặp: không tìm được phim muốn xem, chất lượng 720p của gói Basic không đủ thỏa mãn, thiếu nội dung bản địa phù hợp thị hiếu Châu Á. Dù lý do là gì, kết quả giống nhau: người dùng mở app lên rồi tắt đi mà không xem đủ lâu.

**Giờ xem giảm kéo theo CSAT giảm**

CSAT tháng 7 đạt 4.2/5, tháng 8 rơi xuống 3.8/5 — giảm gần 10%. Người xem ít tự nhiên thất vọng hơn. Họ cảm thấy đang trả tiền hàng tháng nhưng không nhận lại đủ giá trị.

CSAT là chỉ báo sớm (Leading Indicator): nó cảnh báo trước khi người dùng thực sự hành động. Nếu theo dõi kỹ, thấy CSAT tuần đầu tháng 8 đã tụt thì còn cơ hội can thiệp trước khi làn sóng hủy gói ập đến cuối tháng.

**CSAT giảm dẫn đến Churn tăng**

Khi đã thất vọng đủ lâu, quyết định hủy gói chỉ còn là vấn đề thời gian. Tháng 8 ghi nhận 250 nghìn người hủy so với 200 nghìn tháng 7, tăng đúng 25%. Churn Rate leo từ 4.00% lên 5.05%.

Điều đáng lo là Churn Rate là chỉ báo trễ (Lagging Indicator): khi con số này nhảy lên thì thiệt hại đã rồi, tiền đã mất. Vì vậy phải bám chặt CSAT và giờ xem từ sớm thay vì chờ đọc báo cáo cuối tháng mới phát hiện.

---

## 4. Kết Luận: Ba Chỉ Số Cần Theo Dõi Mỗi Tuần

Đừng chỉ nhìn vào Churn Rate khi nó đã tăng. Cần theo dõi tuần tự ba chỉ số theo đúng hướng nhân quả:

1. **Giờ xem TB/User** — Cảnh báo sớm nhất khi người dùng bắt đầu lạnh nhạt.
2. **Điểm CSAT** — Xác nhận sự thất vọng đang tích tụ, báo hiệu làn sóng hủy gói sắp đến.
3. **Churn Rate** — Đo thiệt hại thực tế, đánh giá hiệu quả của các biện pháp đã triển khai.

Giải quyết từ gốc (cải thiện nội dung và chất lượng phát sóng phù hợp với thị trường Châu Á trong gói Basic) bền vững hơn nhiều so với chạy khuyến mãi chắp vá mỗi khi thấy churn tăng.

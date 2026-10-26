# PHÂN TÍCH HÀNH VI KHÁCH HÀNG VÀ ĐỀ XUẤT MARKETING

## 1. Mục tiêu và phạm vi

- Dữ liệu: *Mall Customers*, **200 khách hàng**, 5 cột gốc.
- Mô hình: **K-Means (k = 5)** trên hai trường `Annual Income (k$)` và `Spending Score (1-100)` sau khi chuẩn hóa bằng `StandardScaler`.
- Tuổi và giới tính chỉ được dùng để mô tả, **không quyết định vị trí phân cụm**.
- Không có dữ liệu đơn hàng hoặc doanh thu; các hướng marketing dưới đây là **giả thuyết cần thử nghiệm**, không phải kết luận về lợi nhuận hay ROI.

## 2. Chất lượng dữ liệu

| Tiêu chí | Kết quả |
|---|---:|
| Khách hàng / mã duy nhất | 200 / 200 |
| Giá trị thiếu | 0 |
| Khách hàng trùng mã | 0 |
| Tuổi trung bình | 38,85 |
| Thu nhập trung bình (nghìn USD/năm) | 60,56 |
| Spending Score trung bình | 50,20 / 100 |

## 3. Đánh giá mô hình

So sánh Silhouette trên khoảng k = 2–10 cho điểm cao nhất tại **k = 5**, đạt **0,5547**. Kết quả ARI = 1,00 qua bốn hạt giống khởi tạo trong notebook cho thấy cấu trúc cụm nhất quán trong phép thử hạn chế này. Không được đồng nhất ARI = 1 với hiệu quả marketing hoặc khả năng dự đoán doanh thu.

![Đánh giá Silhouette](../images/silhouette_scores.png)

## 4. Hồ sơ 5 nhóm khách hàng

| Nhóm | Số khách | Tỷ trọng | Thu nhập TB (k$) | Spending Score TB | Tuổi TB |
|---|---:|---:|---:|---:|---:|
| Thu nhập và chi tiêu trung bình | 81 | 40,50% | 55,30 | 49,52 | 42,72 |
| Thu nhập cao – Chi tiêu cao | 39 | 19,50% | 86,54 | 82,13 | 32,69 |
| Thu nhập thấp – Chi tiêu cao | 22 | 11,00% | 25,73 | 79,36 | 25,27 |
| Thu nhập cao – Chi tiêu thấp | 35 | 17,50% | 88,20 | 17,11 | 41,11 |
| Thu nhập thấp – Chi tiêu thấp | 23 | 11,50% | 26,30 | 20,91 | 45,22 |

![Các cụm](../images/customer_clusters.png)

## 5. Phát hiện và giả thuyết tiếp thị

### 5.1. Nhóm thu nhập và chi tiêu trung bình — 81 khách (40,5%)

**Quan sát:** là phân khúc lớn nhất; thu nhập bình quân 55,30 nghìn USD/năm, điểm chi tiêu bình quân 49,52/100. **Giả thuyết thử nghiệm:** chương trình tích điểm, ưu đãi tái mua hoặc thông tin sản phẩm phổ thông có thể tạo phản hồi tốt. Cần đo tỷ lệ chuyển đổi/giữ chân thực tế.

### 5.2. Nhóm thu nhập cao – chi tiêu cao — 39 khách (19,5%)

**Quan sát:** thu nhập bình quân 86,54 nghìn USD/năm, điểm chi tiêu 82,13/100. Đây là nhóm *điểm chi tiêu cao*, **không thể gọi là nhóm đóng góp doanh thu lớn nhất** khi chưa có doanh thu thực tế. **Giả thuyết:** thử nghiệm trải nghiệm thành viên và gợi ý sản phẩm phù hợp, đo tỷ lệ phản hồi so với nhóm đối chứng.

### 5.3. Nhóm thu nhập cao – chi tiêu thấp — 35 khách (17,5%)

**Quan sát:** thu nhập bình quân 88,20 nghìn USD/năm tương đương nhóm trên, nhưng điểm chi tiêu chỉ 17,11/100. Không tự suy đoán nguyên nhân. **Giả thuyết:** dùng khảo sát sở thích/rào cản trải nghiệm, sau đó thử nghiệm thông điệp mới thay vì tự động tăng khuyến mãi.

### 5.4. Nhóm thu nhập thấp – chi tiêu cao — 22 khách (11%)

**Quan sát:** thu nhập bình quân 25,73 nghìn USD/năm, điểm chi tiêu 79,36/100. **Giả thuyết:** thử nghiệm thông tin sản phẩm đúng nhu cầu và ưu đãi minh bạch, tránh suy đoán hoàn cảnh tài chính hoặc đề xuất tín dụng dựa trên điểm nhóm.

### 5.5. Nhóm thu nhập thấp – chi tiêu thấp — 23 khách (11,5%)

**Quan sát:** thu nhập bình quân 26,30 nghìn USD/năm và điểm chi tiêu 20,91/100. **Giả thuyết:** khảo sát nhu cầu, đo tần suất và phản ứng với chương trình giá trị thiết thực. Không kết luận nhóm 'ít tiềm năng' hoặc nên loại khỏi marketing chỉ từ hai đặc trưng.

## 6. Thử nghiệm tiếp theo để tạo giá trị thực tế

1. Thu thập dữ liệu giao dịch (`order_id`, thời gian mua, doanh thu, tần suất và kết quả chiến dịch) có cơ sở đồng ý hợp lệ.
2. Thiết kế A/B test trong từng phân khúc: nhóm thử nghiệm và đối chứng, theo dõi chuyển đổi, doanh thu/khách, tỷ lệ giữ chân và chi phí.
3. Kiểm tra mức chênh lệch và ý nghĩa thực tiễn trước khi triển khai rộng.
4. Theo dõi biến động phân khúc khi có dữ liệu mới; tránh gắn nhãn khách hàng vĩnh viễn.
5. Đánh giá lại việc sử dụng dữ liệu thu nhập/đặc trưng nhân khẩu học để đảm bảo phù hợp pháp luật và giảm rủi ro đối xử bất công.

## 7. Hạn chế

Dữ liệu là mẫu nhỏ với 200 người và không có mục tiêu biến đổi định lượng của chiến dịch. Phân cụm **mô tả cấu trúc dữ liệu**, không tự chứng minh phân khúc nào là 'VIP', đem lại nhiều doanh thu hay thúc đẩy doanh số khi áp dụng khuyến nghị.

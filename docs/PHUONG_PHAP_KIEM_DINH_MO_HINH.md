# PHƯƠNG PHÁP VÀ KIỂM ĐỊNH MÔ HÌNH K-MEANS

## Luồng kỹ thuật

`Mall_Customers.csv` → kiểm tra chất lượng → EDA → chuẩn hóa 2 đặc trưng → K-Means (k=2…10) → so sánh Elbow và Silhouette → chọn k=5 → gắn mô tả tâm cụm → Profile → xuất 3 CSV.

### Dữ liệu đầu vào

Dữ liệu sử dụng **200 người** với `CustomerID`, `Gender`, `Age`, `Annual Income (k$)`, `Spending Score (1-100)`. Chỉ **thu nhập** và **Spending Score** đưa vào K-Means. `CustomerID` là khóa định danh; giới tính/tuổi là thông tin mô tả hậu kiểm.

### Lý do chuẩn hóa

Khoảng cách Euclidean trong K-Means chịu ảnh hưởng của thang đo. `StandardScaler` đưa mỗi biến về đơn vị theo trung bình/độ lệch chuẩn trên tập dữ liệu; tâm cụm được đổi ngược về thang đo gốc để giải thích kinh doanh.

### Lựa chọn số cụm

| k | Inertia | Silhouette Score |
|---:|---:|---:|
| 2 | 269,69 | **0.3213** |
| 3 | 157,70 | **0.4666** |
| 4 | 108,92 | **0.4939** |
| 5 | 65,57 | **0.5547** ← cao nhất |
| 6 | 55,06 | **0.5399** |
| 7 | 44,86 | **0.5281** |
| 8 | 37,15 | **0.4567** |
| 9 | 32,39 | **0.4571** |
| 10 | 29,69 | **0.4362** |

**Giải thích:** `Inertia` thường giảm khi k tăng, do đó không thể chọn k tối ưu bằng việc tìm giá trị nhỏ nhất thuần túy. Silhouette ở k=5 cao nhất trong dải thử nghiệm; sự phù hợp cần kiểm chứng thêm trên tập dữ liệu lớn hơn.

### Đánh giá độ ổn định

Notebook thử các `random_state` 7, 21, 42, 123; màn hình Colab ghi nhận ARI = 1,00 so với seed 42. Đây chỉ là kiểm tra **độ ổn định của phép khởi tạo** trên cùng dữ liệu, không phải đánh giá out-of-sample hay chất lượng chiến dịch.

### Gán nhãn phân khúc

Mã cụm của K-Means tùy thuộc phép gán nội bộ. Notebook gán nhãn bằng so khớp tâm cụm với năm vị trí tham chiếu `thấp-thấp`, `thấp-cao`, `trung bình`, `cao-thấp`, `cao-cao` trong không gian chuẩn hóa; không phụ thuộc cứng Cluster ID. Khi đổi k hoặc đặc trưng, phải đánh giá lại ý nghĩa từng nhóm.

**Môi trường chạy:** Python 3, pandas, numpy, matplotlib, scikit-learn, scipy; Google Colab hoặc Jupyter Notebook. Seed chính `42`, `n_init=20`.

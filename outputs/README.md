# outputs/ — Dữ liệu kết quả từ notebook

| File | Nội dung | Số dòng |
|---|---|---:|
| `Customer_Segmentation_Result.csv` | 200 khách hàng, thêm mã `Cluster` và nhãn `Segment` | 200 |
| `Cluster_Profile.csv` | Số lượng, tỷ trọng và thống kê trung bình/trung vị theo 5 nhóm | 5 |
| `KMeans_Evaluation.csv` | Inertia và Silhouette Score cho k=2…10 | 9 |

**Nguồn:** ba file được người thực hiện xuất từ Google Colab sau khi chạy `Customer_Segmentation_Upgrade.ipynb`; không phải dữ liệu mẫu mô phỏng. Khi chạy lại notebook, kết quả được ghi vào `outputs/` trong thư mục làm việc hiện tại.

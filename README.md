# Dự đoán khách hàng rời bỏ
# 1.Giới thiệu
Dự án này tập trung vào việc phân tích dữ liệu khách hàng của một công ty viễn thông để xây dựng mô hình dự đoán khách hàng có khả năng rời bỏ dịch vụ (churn). Việc dự đoán sớm khách hàng churn giúp công ty triển khai các chiến lược giữ chân phù hợp, giảm thiểu tổn thất doanh thu và duy trì sự phát triển bền vững.

# 2.Mục tiêu
- Khám phá và hiểu rõ dữ liệu khách hàng.
- Làm sạch và tiền xử lý dữ liệu để chuẩn bị cho việc xây dựng mô hình.
- Xây dựng và đánh giá mô hình phân loại để dự đoán churn.
- Cải thiện hiệu suất mô hình, đặc biệt là khả năng phát hiện khách hàng churn.
  
# 3.Bộ dữ liệu
Bộ dữ liệu được sử dụng là customer_churn.csv, chứa thông tin chi tiết về từng khách hàng, bao gồm các thông tin cá nhân, dịch vụ đã đăng ký, thời gian sử dụng dịch vụ, phí hàng tháng, tổng phí và trạng thái churn (Yes/No).

# 4.Các bước thực hiện
- Tải và khám phá dữ liệu: Đọc dữ liệu từ tệp CSV và xem xét cấu trúc, các kiểu dữ liệu và các giá trị duy nhất trong từng cột.
- Làm sạch dữ liệu:
Xóa các cột không cần thiết (customerID).
Kiểm tra và xử lý các bản ghi trùng lặp.
Chuyển đổi kiểu dữ liệu của cột TotalCharges sang dạng số và xử lý các giá trị thiếu (NaN) bằng giá trị trung bình.
Chuẩn hóa các giá trị trong các cột phân loại (ví dụ: thay thế 'No internet service', 'No phone service' bằng 'No').
Chuyển đổi các cột nhị phân ('Yes'/'No', 'Male'/'Female') sang dạng số (1/0).
- Chia dữ liệu: Tách tập dữ liệu thành tập huấn luyện (training set) và tập kiểm tra (testing set).
- Tiền xử lý dữ liệu: Áp dụng các kỹ thuật tiền xử lý như chuẩn hóa dữ liệu số (StandardScaler) và mã hóa one-hot cho các cột phân loại (OneHotEncoder) bằng ColumnTransformer.
- Xây dựng và huấn luyện mô hình Logistic Regression: Sử dụng Pipeline để kết hợp tiền xử lý và mô hình Logistic Regression, sau đó huấn luyện mô hình trên tập dữ liệu huấn luyện.
- Đánh giá mô hình ban đầu: Đánh giá hiệu suất của mô hình bằng báo cáo phân loại (classification_report) và ma trận nhầm lẫn (confusion_matrix).
- Cân bằng dữ liệu với SMOTE: Áp dụng kỹ thuật SMOTE (Synthetic Minority Over-sampling Technique) trên tập dữ liệu huấn luyện đã tiền xử lý để giải quyết vấn đề mất cân bằng lớp (imbalanced data), tăng cường số lượng mẫu của lớp thiểu số (Churn).
- Huấn luyện lại mô hình trên dữ liệu đã cân bằng: Huấn luyện lại mô hình Logistic Regression trên tập dữ liệu huấn luyện đã được cân bằng bằng SMOTE.
- Đánh giá mô hình trên dữ liệu đã cân bằng: Đánh giá hiệu suất của mô hình sau khi áp dụng SMOTE bằng báo cáo phân loại và ma trận nhầm lẫn, so sánh kết quả với mô hình ban đầu.

# 5.Kết quả
- Mô hình Logistic Regression ban đầu đạt độ chính xác tổng thể 81%, nhưng gặp khó khăn trong việc phát hiện khách hàng churn (Recall cho lớp Churn thấp).
-Sau khi áp dụng SMOTE, Recall cho lớp Churn đã được cải thiện đáng kể, tuy nhiên độ chính xác tổng thể và Precision cho lớp Churn có thể giảm do sự đánh đổi giữa việc giảm False Negative và tăng False Positive.
- Kết quả chi tiết và trực quan hóa ma trận nhầm lẫn được trình bày trong notebook.


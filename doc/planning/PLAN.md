# Kế hoạch đồ án MoviesDataset

Đọc [đề Final Project](../CSC17104_2026_Final_Project.pdf) để đối chiếu yêu cầu và xem [README](../../README.md) để tải CSV, tạo môi trường và mở Jupyter. Đây là kế hoạch nội bộ của hai thành viên.

## Việc làm tiếp theo

- [ ] **Chuẩn bị cả hai máy.** Kiểm tra môi trường `movies-dataset`, tải cùng bản CSV và đặt vào `data/raw/` theo README. Xác nhận bộ dữ liệu đã được giảng viên duyệt.
- [x] **Khám phá dữ liệu — cập nhật theo câu hỏi (17/11/2026).** [01_collection_exploration.ipynb](../../notebooks/01_collection_exploration.ipynb) đã chạy từ đầu với 18 cell code, 8 hình. Có bảng sử dụng cột, kiểm tra chất lượng, mẫu riêng Q1–Q4, độ phủ Q2 theo thời gian, thời lượng Q3 theo nhóm và độ phủ tài chính Q4. Xem [ghi nhận bàn giao](data-exploration/task.md#cập-nhật-ngày-17112026). Thông tin đơn vị và phạm vi tài chính của CSV cần được xác minh trước khi phân tích Q4.
- [x] **Chốt 4 câu hỏi.** Đã ghi câu hỏi, động cơ, người phụ trách, phạm vi và tiêu chí dự kiến tại [QUESTIONS.md](../QUESTIONS.md). Khang phụ trách Q1, Q2 (ML), Khánh phụ trách Q3, Q4.
- [ ] **Phân tích các câu không dùng ML.** Làm trong `02_analysis.ipynb`. Ghi cách xử lý và số dòng sau mỗi bước thay đổi dữ liệu. Mỗi câu áp dụng ít nhất hai tiêu chí D1–D6 và các câu không dùng ML cộng lại phủ ít nhất bốn tiêu chí khác nhau.
- [ ] **Thực hiện câu ML.** Làm trong `03_ml_question.ipynb`. Xác định mục tiêu và thời điểm dự đoán, kiểm tra rò rỉ dữ liệu, chọn cách chia tập phù hợp, rồi so sánh ít nhất hai mô hình và một baseline. Tiền xử lý trong `Pipeline`, tinh chỉnh bằng cross-validation chỉ trên tập train và đánh giá tập test một lần. Phân tích lỗi và diễn giải mô hình để trả lời câu hỏi.
- [ ] **Rà soát bài nộp.** Mỗi câu có ít nhất hai biểu đồ có nhãn, kết luận bằng số liệu và nêu giới hạn. Chạy lại notebook theo thứ tự, cập nhật README và nhật ký LLM, tự viết reflection, chuẩn bị `slides.pdf` và tập hỏi đáp.

## Phân công câu hỏi

| Câu | Người phụ trách | Câu hỏi đã chốt | Tiêu chí D hoặc ML | Trạng thái |
| --- | --- | --- | --- | --- |
| Q1 | Khang | IMDb và TMDB chấm điểm lệch nhau như thế nào? | D3, D4, D5, D6 | Đã chốt, chờ phân tích |
| Q2 | Khang | Nhìn hồ sơ phim, đoán khán giả IMDb chấm mấy điểm? | ML | Đã chốt, chờ mô hình |
| Q3 | Khánh | Phim có ngày càng dài hơn không? | D2, D4, D5, D6 | Đã chốt, chờ phân tích |
| Q4 | Khánh | Cùng mức ngân sách, thể loại phim nào thường có doanh thu cao hơn? | D4, D5, D6 | Đã chốt, cần xác minh tài chính và phân tích |

Phạm vi và phương án chi tiết của từng câu được theo dõi trong [QUESTIONS.md](../QUESTIONS.md).

## Bàn giao công việc và nhờ AI hỗ trợ

Khi xong một việc hoặc đổi hướng, cập nhật checkbox và trạng thái ở đây. Khi bàn giao, ghi việc đã làm, link notebook hoặc commit, vấn đề còn vướng và bước tiếp theo. Khi nhờ AI, đưa file kế hoạch này cùng phần đề và notebook liên quan để AI hiểu đúng câu hỏi đang làm.

Theo mục 6 của đề, dùng AI như gia sư để giải thích khái niệm, lỗi hoặc hàm thư viện. Hai thành viên tự viết phần phân tích, câu trả lời và reflection. Ghi những lần sử dụng đáng kể vào [LLM_USAGE.md](../../LLM_USAGE.md).

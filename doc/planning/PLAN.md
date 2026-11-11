# Kế hoạch đồ án MoviesDataset

Đọc [đề Final Project](../CSC17104_2026_Final_Project.pdf) để đối chiếu yêu cầu và xem [README](../../README.md) để tải CSV, tạo môi trường và mở Jupyter. Đây là kế hoạch nội bộ của hai thành viên.

## Việc làm tiếp theo

- [ ] **Chuẩn bị cả hai máy.** Kiểm tra môi trường `movies-dataset`, tải cùng bản CSV và đặt vào `data/raw/` theo README. Xác nhận bộ dữ liệu đã được giảng viên duyệt.
- [ ] **Khám phá dữ liệu.** Tạo `01_collection_exploration.ipynb` khi bắt đầu làm. Ghi nguồn, giấy phép, số dòng và cột, ý nghĩa mỗi dòng, dữ liệu thiếu, trùng và giá trị bất thường. Chốt 3–5 quan sát chính để làm cơ sở chọn câu hỏi.
- [ ] **Chốt 4 câu hỏi.** Mỗi thành viên phụ trách hai câu. Chọn ít nhất một câu dùng ML và kiểm tra các câu còn lại có đủ chiều sâu theo đề.
- [ ] **Phân tích các câu không dùng ML.** Làm trong `02_analysis.ipynb`. Ghi cách xử lý và số dòng sau mỗi bước thay đổi dữ liệu. Mỗi câu áp dụng ít nhất hai tiêu chí D1–D6 và các câu không dùng ML cộng lại phủ ít nhất bốn tiêu chí khác nhau.
- [ ] **Thực hiện câu ML.** Làm trong `03_ml_question.ipynb`. Xác định mục tiêu và thời điểm dự đoán, kiểm tra rò rỉ dữ liệu, chọn cách chia tập phù hợp, rồi so sánh ít nhất hai mô hình và một baseline. Tiền xử lý trong `Pipeline`, tinh chỉnh bằng cross-validation chỉ trên tập train và đánh giá tập test một lần. Phân tích lỗi và diễn giải mô hình để trả lời câu hỏi.
- [ ] **Rà soát bài nộp.** Mỗi câu có ít nhất hai biểu đồ có nhãn, kết luận bằng số liệu và nêu giới hạn. Chạy lại notebook theo thứ tự, cập nhật README và nhật ký LLM, tự viết reflection, chuẩn bị `slides.pdf` và tập hỏi đáp.

## Phân công câu hỏi

| Câu | Người phụ trách | Câu hỏi đã chốt | Tiêu chí D hoặc ML | Trạng thái |
| --- | --- | --- | --- | --- |
| Q1 | Thành viên 1 (dự kiến) | Chưa chốt | Chưa xác định | Chờ EDA |
| Q2 | Thành viên 1 (dự kiến) | Chưa chốt | Chưa xác định | Chờ EDA |
| Q3 | Thành viên 2 (dự kiến) | Chưa chốt | Chưa xác định | Chờ EDA |
| Q4 | Thành viên 2 (dự kiến) | Chưa chốt | Chưa xác định | Chờ EDA |

Sau khi chốt, thay nhãn thành viên bằng tên thật và ghi phân công chính thức trong README.

## Bàn giao công việc và nhờ AI hỗ trợ

Khi xong một việc hoặc đổi hướng, cập nhật checkbox và trạng thái ở đây. Khi bàn giao, ghi việc đã làm, link notebook hoặc commit, vấn đề còn vướng và bước tiếp theo. Khi nhờ AI, đưa file kế hoạch này cùng phần đề và notebook liên quan để AI hiểu đúng câu hỏi đang làm.

Theo mục 6 của đề, dùng AI như gia sư để giải thích khái niệm, lỗi hoặc hàm thư viện. Hai thành viên tự viết phần phân tích, câu trả lời và reflection. Ghi những lần sử dụng đáng kể vào [LLM_USAGE.md](../../LLM_USAGE.md).

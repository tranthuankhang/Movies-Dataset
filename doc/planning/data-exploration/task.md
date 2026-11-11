# Khám phá dữ liệu phim từ CSV raw

**Người phụ trách** · Điền tên thành viên nhận việc

**Hạn bàn giao** · Nhóm thống nhất khi giao việc

Khám phá bản CSV nhóm tải từ Kaggle để hiểu mỗi dòng đại diện cho gì, cột nào dùng được và vấn đề nào cần xử lý trước khi chốt câu hỏi.

**Đầu vào** · `data/raw/TMDB  IMDB Movies Dataset.csv` (hai dấu cách giữa `TMDB` và `IMDB`). Giữ nguyên CSV gốc.

**Bàn giao** · `notebooks/01_collection_exploration.ipynb` chạy được từ CSV raw, có kết quả kiểm tra và nhận xét ngắn bằng Markdown.

## Trước khi bắt đầu

1. Đọc [README mục 2](../../../README.md#2-tải-dữ-liệu) để lấy đúng bản CSV và [mục 8](../../../README.md#8-cấu-trúc-repository-và-cách-chạy) để thiết lập môi trường Conda, đăng ký kernel và mở JupyterLab.
2. Đọc **mục 3.1 “Data collection” và mục 3.2 “Data exploration” (trang 2)** của [đề CSC17104 Final Project](../../CSC17104_2026_Final_Project.pdf). Dùng mục 3.1 để viết phần nguồn và bối cảnh, mục 3.2 để đối chiếu nội dung khám phá raw. Nếu dùng LLM hỗ trợ, đọc thêm mục 6 (trang 5) và ghi vào [nhật ký LLM](../../../LLM_USAGE.md) theo đề.
3. Từ thư mục gốc repo, chạy `conda activate movies-dataset` rồi mở JupyterLab bằng `jupyter lab`. Tạo `notebooks/01_collection_exploration.ipynb` nếu chưa có và chọn kernel **Python (movies-dataset)**. Dùng môi trường này cho toàn bộ phần đọc CSV, khám phá và vẽ biểu đồ. Dùng đường dẫn tương đối đến CSV theo README để thành viên còn lại có thể chạy lại.

## Checklist

- [ ] **Nguồn và bối cảnh.** Ghi chủ đề, nguồn và URL, người công bố, ngày công bố nếu xác minh được, giấy phép, cách TMDB và IMDb được kết hợp, phạm vi và giới hạn đã biết, lý do chọn bộ dữ liệu. Phân biệt ngày công bố với ngày nhóm tải CSV.
- [ ] **Cấu trúc và bản ghi trùng.** Đếm số dòng, số cột và dòng rỗng nếu có. Giải thích đơn vị của mỗi dòng, ý nghĩa và kiểu dữ liệu của các cột. Đếm dòng trùng toàn bộ, kiểm tra trùng `id` và `tconst` trên các giá trị có mã, rồi ghi cột nào dự kiến chuyển kiểu hoặc bỏ và vì sao.
- [ ] **Dữ liệu thiếu.** Lập bảng số lượng và tỷ lệ thiếu theo cột. Xem các cột quan trọng có hay thiếu cùng nhau hoặc tập trung ở nhóm phim nào. Ghi hướng xử lý cho các cột sẽ dùng và đánh dấu nguyên nhân chưa xác minh.
- [ ] **Cột số.** Xem phân phối, giá trị điển hình, độ phân tán và các giá trị cực trị của `budget`, `revenue`, `runtime`, điểm và lượt chấm. Đếm riêng số `0` ở `budget` và `revenue` để xem xét khả năng chúng là giá trị quy ước cho dữ liệu thiếu.
- [ ] **Cột phân loại và định dạng.** Xem số lượng giá trị khác nhau, nhóm phổ biến, nhãn hiếm hoặc thiếu nhất quán ở vài cột như `original_language` và `status`. Kiểm tra cách biểu diễn phim có nhiều `genres` và thử xác định số giá trị `release_date` không đọc được thành ngày.
- [ ] **Mối liên hệ sơ bộ.** Chọn vài cặp cột liên quan để xem bằng biểu đồ, tương quan, bảng chéo hoặc thống kê theo nhóm. Ví dụ, xem điểm IMDb theo số lượt chấm hoặc xem ngân sách và doanh thu trên các dòng có cả hai số liệu. Ghi điều kiện chọn mẫu và số dòng dùng nếu chỉ xem một phần dữ liệu.
- [ ] **Tóm tắt cuối notebook.** Ghi 3–5 quan sát có số liệu, vấn đề chất lượng đáng kể, cách tiền xử lý dự kiến và những mẫu hình có thể dẫn đến câu hỏi. Dừng ở mức quan sát và đề xuất cho bước đặt câu hỏi của nhóm.

Tập trung vào các cột liên quan đến hướng câu hỏi trong README và tóm tắt ngắn các cột còn lại. Chọn biểu đồ khi chúng giúp đọc phân phối hoặc nhận ra một mẫu hình.

## Khi bàn giao

- [ ] Khởi động lại kernel **Python (movies-dataset)**, chạy toàn bộ cell theo thứ tự với bản CSV raw của nhóm và lưu notebook sau khi chạy. Kiểm tra các bảng, biểu đồ và nhận xét khớp với kết quả.
- [ ] Gửi đường dẫn notebook hoặc commit, kèm các điểm cần nhóm thống nhất trước khi chốt câu hỏi. Đánh dấu phần khám phá trong [PLAN.md](../PLAN.md) khi bàn giao xong.

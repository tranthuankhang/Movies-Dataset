# Khám phá dữ liệu phim từ CSV raw

**Người phụ trách** · Điền tên thành viên nhận việc

**Hạn bàn giao** · Nhóm thống nhất khi giao việc

Khám phá bản CSV nhóm tải từ Kaggle để hiểu mỗi dòng đại diện cho gì, cột nào dùng được và vấn đề nào cần xử lý trước khi chốt câu hỏi.

**Đầu vào** · `data/raw/TMDB  IMDB Movies Dataset.csv` (hai dấu cách giữa `TMDB` và `IMDB`). Giữ nguyên CSV gốc.

**Bàn giao** · Tạo và chạy `notebooks/01_collection_exploration.ipynb` từ CSV raw. Ghi kết quả kiểm tra và nhận xét ngắn bằng Markdown trong notebook.

## Trước khi bắt đầu

1. Đọc [README mục 2](../../../README.md#2-tải-dữ-liệu) và [mục 8](../../../README.md#8-cấu-trúc-repository-và-cách-chạy) để làm theo hướng dẫn tải dữ liệu và chạy dự án.
2. Đọc **mục 3.1 “Data collection” và mục 3.2 “Data exploration” (trang 2)** của [đề CSC17104 Final Project](../../CSC17104_2026_Final_Project.pdf). Dùng mục 3.1 để viết phần nguồn và bối cảnh, mục 3.2 để đối chiếu nội dung khám phá raw. Nếu dùng LLM hỗ trợ, đọc thêm mục 6 (trang 5) và ghi vào [nhật ký LLM](../../../LLM_USAGE.md) theo đề.

## Checklist

- [x] **Nguồn và bối cảnh.** Ghi chủ đề, nguồn và URL, người công bố, ngày công bố nếu xác minh được, giấy phép, cách TMDB và IMDb được kết hợp, phạm vi và giới hạn đã biết, lý do chọn bộ dữ liệu. Phân biệt ngày công bố với ngày nhóm tải CSV.
- [x] **Cấu trúc và bản ghi trùng.** Đếm số dòng, số cột và dòng rỗng nếu có. Giải thích đơn vị của mỗi dòng, ý nghĩa và kiểu dữ liệu của các cột. Đếm dòng trùng toàn bộ, kiểm tra trùng `id` và `tconst` trên các giá trị có mã, rồi ghi cột nào dự kiến chuyển kiểu hoặc bỏ và vì sao.
- [x] **Dữ liệu thiếu.** Lập bảng số lượng và tỷ lệ thiếu theo cột. Xem các cột quan trọng có hay thiếu cùng nhau hoặc tập trung ở nhóm phim nào. Ghi hướng xử lý cho các cột sẽ dùng và đánh dấu nguyên nhân chưa xác minh.
- [x] **Cột số.** Xem phân phối, giá trị điển hình, độ phân tán và các giá trị cực trị của `budget`, `revenue`, `runtime`, điểm và lượt chấm. Đếm riêng số `0` ở `budget` và `revenue` để xem xét khả năng chúng là giá trị quy ước cho dữ liệu thiếu.
- [x] **Cột phân loại và định dạng.** Xem số lượng giá trị khác nhau, nhóm phổ biến, nhãn hiếm hoặc thiếu nhất quán ở vài cột như `original_language` và `status`. Kiểm tra cách biểu diễn phim có nhiều `genres` và thử xác định số giá trị `release_date` không đọc được thành ngày.
- [x] **Mối liên hệ sơ bộ.** Chọn vài cặp cột liên quan để xem bằng biểu đồ, tương quan, bảng chéo hoặc thống kê theo nhóm. Ví dụ, xem điểm IMDb theo số lượt chấm hoặc xem ngân sách và doanh thu trên các dòng có cả hai số liệu. Ghi điều kiện chọn mẫu và số dòng dùng nếu chỉ xem một phần dữ liệu.
- [x] **Tóm tắt cuối notebook.** Ghi 3–5 quan sát có số liệu, vấn đề chất lượng đáng kể, cách tiền xử lý dự kiến và những mẫu hình có thể dẫn đến câu hỏi. Dừng ở mức quan sát và đề xuất cho bước đặt câu hỏi của nhóm.

Tập trung vào các cột liên quan đến hướng câu hỏi trong README và tóm tắt ngắn các cột còn lại. Chọn biểu đồ khi chúng giúp đọc phân phối hoặc nhận ra một mẫu hình.

## Khi bàn giao

- [x] Chạy lại toàn bộ notebook từ đầu với bản CSV raw của nhóm rồi lưu kết quả. Kiểm tra các bảng, biểu đồ và nhận xét khớp với kết quả chạy.
- [x] Gửi đường dẫn notebook hoặc commit, kèm các điểm cần nhóm thống nhất trước khi chốt câu hỏi. Đánh dấu phần khám phá trong [PLAN.md](../PLAN.md) khi bàn giao xong.

## Tiến độ ngày 15/11/2026

- Đã hoàn tất [notebook khám phá](../../../notebooks/01_collection_exploration.ipynb), chạy từ đầu trong `movies-dataset`: **13 cell code, 5 hình**, không có lỗi hoặc cảnh báo trong output. SHA-256 nguồn trước/sau chạy khớp nhau, giữ nguyên CSV raw. Đã kiểm tra bảng và hình; bàn giao qua đường dẫn notebook.
- Kiểm tra ban đầu: 443.656 dòng, 29 cột, không trùng toàn bộ dòng; có 13.894 dòng dư theo `id`, 16.995 dòng dư theo `tconst`, 1.424 mã IMDb liên kết nhiều `id` TMDB.
- **Quyết định 1 — đã chọn A:** toàn bộ raw cho kiểm tra chất lượng; quan hệ sơ bộ dùng 425.189 dòng có cả `id` và `tconst` xuất hiện đúng một lần. Ưu: tránh đếm lặp mà chưa cần đoán cách gộp. Nhược: loại cả một số phim chỉ khác danh sách diễn viên và có thể làm lệch mẫu.
- **Quyết định 2 — đã chọn A:** chỉ tính quan hệ tài chính khi `budget > 0` và `revenue > 0`, còn **10.165 dòng** (2,29% raw). Ưu: tránh dùng số 0 chưa rõ ý nghĩa. Nhược: mẫu nhỏ và có thể thiên lệch. Spearman ngân sách–doanh thu **0,770**; chưa kiểm soát thời gian, thể loại hoặc khác biệt đơn vị tiền tệ.
- **Quyết định 3 — đã chọn A:** so sánh điểm trên mẫu hợp lệ có lượt ở cả hai nền tảng, rồi dùng ngưỡng 10/100/1.000 lượt. Số mẫu lần lượt **267.113 / 77.681 / 18.056 / 3.930**. Ưu: thấy độ nhạy. Nhược: các mẫu lồng nhau, thành phần phim thay đổi. Chênh lệch trung bình TMDB−IMDb đổi từ **−0,282** điểm ở mẫu có lượt thành **+0,066** điểm ở ngưỡng 1.000.
- **Trước khi chốt câu hỏi:** nhóm thống nhất phạm vi phim điện ảnh/phim ngắn/truyền hình; có điều tra và gộp mã lặp để giữ thêm phim không; ngưỡng lượt chấm chính cho từng câu; cách kiểm chứng tài chính 0, cực trị và khác biệt qua thời gian. Các quyết định này thuộc bước phân tích tiếp theo, chưa áp dụng như quy tắc làm sạch chung.
- **Bước tiếp theo:** chọn bốn câu hỏi trong `PLAN.md`, phân công hai câu mỗi thành viên và ít nhất một câu ML. Nhóm tự viết, rà soát phần phân tích bài nộp theo mục 6 của đề; phần hỗ trợ đã ghi trong `LLM_USAGE.md`.

## Cập nhật ngày 17/11/2026

- Đã điều chỉnh notebook 01 theo bốn câu hỏi tại [QUESTIONS.md](../../QUESTIONS.md), đối chiếu năm nhóm yêu cầu của mục 3.2 trong đề. Có bảng liên hệ câu hỏi–cột dữ liệu, bảng chất lượng và luồng lọc riêng cho từng câu, tám hình cùng năm quan sát cuối notebook.
- Chạy lại từ đầu trong `movies-dataset` với **18 cell code và 8 hình**, không có lỗi hoặc cảnh báo trong output. Các kiểm tra số dòng, mẫu theo thời gian và SHA-256 nguồn đều đạt.
- Q1 có **55.418 cặp** ở ngưỡng 10 lượt và **14.559 cặp** ở ngưỡng 100 trong phạm vi 1990–2024. Q2 có **363.368 tác phẩm trước 2020** và **45.267 tác phẩm 2020–2024**, với bảng độ đầy đủ đầu vào cho cả hai khoảng thời gian.
- Q3 có **209.322 tác phẩm** trong mẫu sơ bộ, kèm thống kê thời lượng, số mẫu theo giai đoạn, thể loại và ngôn ngữ. Q4 có **8.049 tác phẩm**, kèm phân phối tài chính và bảng số mẫu theo thể loại–giai đoạn–nhóm ngân sách.
- Đã đọc mô tả từ hai nguồn Kaggle nhưng chưa xác minh được đơn vị, phạm vi doanh thu và cách chuẩn hóa tài chính của bản v578. Notebook ghi nhãn giá trị CSV và nêu giới hạn này. Phân tích Q4 cần làm rõ thông tin tài chính trước khi diễn giải chênh lệch tiền tệ.
- Bổ sung bảng so sánh cờ IQR với z-score `|z| > 3` dùng `ddof=0` trên cùng mẫu từng cột. Thêm heatmap Spearman tám cột trên **7.779 tác phẩm** thuộc mẫu Q4 có đủ giá trị hợp lệ, với số dòng sau từng bước lọc và cùng số tác phẩm cho mọi cặp hệ số.
- Bước tiếp theo là tiền xử lý và phân tích Q1, Q3, Q4 trong notebook 02, xây dựng Pipeline và đánh giá mô hình Q2 trong notebook 03 theo phạm vi đã chốt.

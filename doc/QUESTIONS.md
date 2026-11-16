# Câu hỏi phân tích của nhóm

Theo mục 3.3 của đề, nhóm hai người có **4 câu hỏi tổng cộng**. Mỗi thành viên phụ trách **2 câu** và ít nhất **1 trong 4 câu** dùng học máy (ML). [Đề Final Project, trang 2–4](CSC17104_2026_Final_Project.pdf)

Bảng dưới đây dùng phương án **3 câu non-ML và 1 câu ML** làm khung để hai thành viên thảo luận. Sau khi thống nhất, cập nhật danh sách câu hỏi và người phụ trách trong [README](../README.md#6-câu-hỏi-phân-tích-dự-kiến).

| Câu | Loại | Người phụ trách | Câu hỏi đã chốt |
| --- | --- | --- | --- |
| Q1 | Non-ML | Khang | IMDb và TMDb chấm điểm lệch nhau như thế nào? |
| Q2 | ML | Khang | Nhìn hồ sơ phim, đoán khán giả IMDb chấm mấy điểm? |
| Q3 | Non-ML | Khánh | |
| Q4 | Non-ML | Khánh | |

## Cách điền

- **Câu hỏi** — viết thành một câu cụ thể, nêu biến cần phân tích hoặc dự đoán và phạm vi so sánh khi có liên quan. Kiểm tra xem dữ liệu hiện có đủ để trả lời hay không.
- **Động cơ** — giải thích vì sao câu hỏi đáng trả lời, ai sẽ quan tâm và kết quả giúp họ đưa ra quyết định gì.
- **Câu non-ML** — chọn ít nhất **2 tiêu chí D1–D6** cho mỗi câu và ghi rõ sẽ thực hiện từng tiêu chí ra sao. Các câu non-ML cộng lại phải phủ ít nhất **4 tiêu chí khác nhau**.
- **Câu ML** — nêu rõ dự đoán gì, cho ai, vào thời điểm nào và dùng được những thông tin nào tại thời điểm đó.

| Tiêu chí | Cách áp dụng |
| --- | --- |
| D1 | Ghép thêm bảng hoặc bộ dữ liệu và kiểm tra số dòng trước, sau khi ghép cùng các khóa chưa khớp. |
| D2 | Định hình lại bảng hoặc phân tích theo thời gian, chẳng hạn so sánh giữa các giai đoạn. |
| D3 | Tạo biến mới từ các cột gốc và giải thích vì sao cần biến đó. |
| D4 | Kiểm tra mối liên hệ trong các nhóm hoặc sau khi kiểm soát một biến khác. |
| D5 | Định lượng độ bất định hoặc độ lớn hiệu ứng bằng khoảng tin cậy, kiểm định hoặc thước đo hiệu ứng. |
| D6 | Kiểm tra kết luận có đổi khi dùng một quy tắc hợp lý khác về làm sạch, ngưỡng ngoại lệ hoặc khoảng thời gian. |

## Q1 – IMDb và TMDb chấm điểm lệch nhau như thế nào? (Khang, non-ML)

- **Câu hỏi** — Trên những phim có lượt chấm ở cả IMDb và TMDb, hai nền tảng chấm lệch nhau bao nhiêu, bên nào thường chấm cao hơn, và mức lệch có khác nhau giữa các thể loại không?
- **Động cơ, người quan tâm và quyết định** — Người tổng hợp đánh giá phim có thể dùng kết quả để biết khi nào nên đối chiếu điểm ở cả hai nền tảng.
- **Cột và phạm vi dữ liệu dự kiến** — Ghép cặp `vote_average` và `averageRating` trên cùng tác phẩm. Dùng `vote_count` và `numVotes` để đặt ngưỡng lượt chấm, `genres` để chia nhóm và `release_date` để giới hạn phạm vi phát hành 1990–2024. Dùng `id` và `tconst` để xử lý bản ghi trùng.
- **D3** — Tính chênh lệch `điểm TMDb − điểm IMDb` và trị tuyệt đối của chênh lệch. Tổng hợp trên toàn bộ mẫu rồi xem theo thể loại.
- **D4** — Kiểm tra kết luận chung về mức lệch và bên chấm cao hơn có còn giữ trong từng thể loại. Khi so các thể loại, có thể xét trong cùng giai đoạn phát hành để giảm ảnh hưởng của sự khác nhau về năm phát hành.
- **D5** — Ước lượng khoảng tin cậy 95% cho chênh lệch bằng bootstrap theo phim, giữ hai điểm của mỗi phim đi chung.
- **D6** — So sánh kết quả khi yêu cầu ít nhất **10 lượt** và **100 lượt** ở cả hai nền tảng.

## Q2 – Nhìn hồ sơ phim, đoán khán giả IMDb chấm mấy điểm? (Khang, ML)

- **Câu hỏi** — Dựa vào thể loại, thời lượng, ngôn ngữ gốc và năm phát hành, mô hình có thể dự đoán điểm IMDb của một tác phẩm chính xác đến đâu?
- **Động cơ, người dùng và quyết định** — Người quản lý danh mục phim có thể dùng mô hình để xem hồ sơ phim cung cấp bao nhiêu thông tin về điểm khán giả IMDb khi chưa tra cứu điểm thực tế.
- **Biến mục tiêu và thời điểm dự đoán** — Dự đoán `averageRating` khi đã có hồ sơ phim và chưa tra cứu điểm IMDb.
- **Cột đầu vào** — `genres`, `runtime`, `original_language` và năm trích từ `release_date`. Loại điểm, lượt chấm và chỉ số phổ biến khỏi đầu vào để mô hình chỉ dùng thông tin hồ sơ đã nêu.
- **Cách chia dữ liệu dự kiến** — Dùng các năm phát hành trước 2020 để huấn luyện và 2020–2024 để kiểm tra, sau khi xử lý bản ghi trùng.
- **Đánh giá** — Dùng MAE để đo sai số theo đơn vị điểm IMDb. So sánh ít nhất hai mô hình và một baseline, tiền xử lý trong `Pipeline`, tinh chỉnh bằng cross-validation trên tập huấn luyện và đánh giá tập kiểm tra một lần.
- **Phân tích lỗi và diễn giải mô hình** — Kiểm tra mô hình sai nhiều ở nhóm phim hoặc khoảng điểm nào, rồi giải thích kết quả dựa trên những đặc điểm trong hồ sơ phim.

## Q3 – Non-ML (Khánh)

- **Câu hỏi** — …
- **Động cơ, người quan tâm và quyết định** — …
- **Cột và phạm vi dữ liệu** — …
- **Tiêu chí D1–D6 và cách áp dụng** — …

## Q4 – Non-ML (Khánh)

- **Câu hỏi** — …
- **Động cơ, người quan tâm và quyết định** — …
- **Cột và phạm vi dữ liệu** — …
- **Tiêu chí D1–D6 và cách áp dụng** — …

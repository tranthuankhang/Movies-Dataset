# Câu hỏi phân tích của nhóm

Theo mục 3.3 của đề, nhóm hai người có **4 câu hỏi tổng cộng**. Mỗi thành viên phụ trách **2 câu** và ít nhất **1 trong 4 câu** dùng học máy (ML). [Đề Final Project, trang 2–4](CSC17104_2026_Final_Project.pdf)

Bảng dưới đây dùng phương án **3 câu non-ML và 1 câu ML** làm khung để hai thành viên thảo luận. Sau khi thống nhất, cập nhật danh sách câu hỏi và người phụ trách trong [README](../README.md#6-câu-hỏi-phân-tích-dự-kiến).

| Câu | Loại | Người phụ trách | Câu hỏi đã chốt |
| --- | --- | --- | --- |
| Q1 | Non-ML | Khang | IMDb và TMDb chấm điểm lệch nhau như thế nào? |
| Q2 | ML | Khang | Nhìn hồ sơ phim, đoán khán giả IMDb chấm mấy điểm? |
| Q3 | Non-ML | Khánh | Phim có ngày càng dài hơn không? |
| Q4 | Non-ML | Khánh | Cùng mức ngân sách, thể loại phim nào thường có doanh thu cao hơn? |

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

## Q3 – Phim có ngày càng dài hơn không? (Khánh, non-ML)

- **Câu hỏi** — Trong các tác phẩm phát hành giai đoạn 1990–2024 của dataset, thời lượng thay đổi thế nào qua các giai đoạn? Xu hướng chung có còn xuất hiện khi xét riêng từng thể loại và nhóm ngôn ngữ gốc không?
- **Vì sao đáng trả lời** — Thời lượng ảnh hưởng trực tiếp đến thời gian cần dành cho một buổi chiếu. Hiểu phân phối thời lượng và sự thay đổi theo giai đoạn, thể loại giúp người tổ chức có cơ sở ước lượng thời gian khi xây dựng một chương trình giới thiệu phim.
- **Ai quan tâm** — Người tổ chức câu lạc bộ phim, buổi chiếu chuyên đề hoặc chương trình giới thiệu tác phẩm theo thể loại và thời kỳ.
- **Quyết định được hỗ trợ** — Chọn khung thời gian cho chương trình và khoanh vùng thể loại, giai đoạn để tìm các tác phẩm phù hợp. Kết quả thống kê giúp lập danh sách ứng viên ban đầu, sau đó người tổ chức kiểm tra thời lượng cụ thể của từng tác phẩm và thời gian thảo luận dự kiến.
- **Cột và phạm vi dữ liệu dự kiến** — Dùng `runtime`, `release_date`, `genres`, `original_language`, `status`, `id` và `tconst`. Bắt đầu với tác phẩm `Released`, phát hành 1990–2024, có thời lượng dương, có thể loại và cả hai mã xuất hiện đúng một lần trong raw. Kiểm tra sơ bộ ngày 17/11/2026 có **209.322 bản ghi** đáp ứng các điều kiện này. Phạm vi và cách xử lý các trường hợp bất thường sẽ được rà lại khi khám phá các cột liên quan.
- **D2** — Tạo năm phát hành, tổng hợp thời lượng trung vị theo năm hoặc giai đoạn và dùng bảng pivot để so sánh các thể loại qua thời gian. Ghi rõ số mẫu, đặc biệt khi so giai đoạn 2020–2024 với các giai đoạn dài hơn.
- **D4** — Kiểm tra xu hướng thời lượng trong từng thể loại và nhóm ngôn ngữ để xem sự thay đổi của thành phần tác phẩm có ảnh hưởng đến xu hướng chung hay không.
- **D5** — Ước lượng khoảng tin cậy 95% cho chênh lệch thời lượng trung vị giữa các giai đoạn bằng bootstrap theo tác phẩm. Diễn giải chênh lệch bằng phút để người nghe dễ hình dung.
- **D6** — So sánh kết quả trên toàn bộ thời lượng dương với một phạm vi thời lượng hợp lý được chọn và giải thích sau khi kiểm tra phân phối, ví dụ khi xem riêng các tác phẩm dài ít nhất 60 phút. Báo cáo tác động của quy tắc này đến số mẫu và kết luận.
- **Cách trình bày dự kiến** — Một biểu đồ cho xu hướng thời lượng qua thời gian, một biểu đồ so sánh các giai đoạn trong từng thể loại. Nêu mức thay đổi bằng phút cùng số mẫu.
- **Giới hạn cần giải thích** — CSV thiếu `titleType`, nên phạm vi gồm nhiều loại tác phẩm. Thể loại có nhiều nhãn và thời lượng có số 0, cực trị. Các thống kê theo thể loại cần đếm mỗi nhãn một lần trên mỗi tác phẩm, còn bootstrap cần lấy mẫu theo tác phẩm để giữ các nhãn đi cùng nhau.

## Q4 – Cùng mức ngân sách, thể loại phim nào thường có doanh thu cao hơn? (Khánh, non-ML)

- **Câu hỏi** — Trong các tác phẩm phát hành giai đoạn 1990–2024 có ghi nhận ngân sách và doanh thu dương, doanh thu khác nhau thế nào giữa các thể loại khi so sánh những tác phẩm có mức ngân sách và giai đoạn phát hành tương đồng?
- **Vì sao đáng trả lời** — Doanh thu thường được dùng khi đánh giá quy mô thương mại của phim. Đặt doanh thu cạnh ngân sách và thời kỳ phát hành giúp xem xét sự khác biệt giữa các thể loại trong những nhóm tác phẩm có quy mô sản xuất tương đồng.
- **Ai quan tâm** — Người nghiên cứu thị trường phim và nhóm lập kế hoạch sản xuất cần tìm các tác phẩm tương đồng để tham khảo kết quả doanh thu đã ghi nhận.
- **Quyết định được hỗ trợ** — Chọn nhóm phim tham chiếu cho một ý tưởng dự án và xác định những thể loại cần nghiên cứu thị trường sâu hơn với quy mô ngân sách dự kiến. Các khoảng doanh thu và mức phân tán giúp xây dựng kỳ vọng tham khảo có tính đến sự khác nhau giữa các tác phẩm.
- **Cột và phạm vi dữ liệu dự kiến** — Dùng `budget`, `revenue`, `genres`, `release_date`, `status`, `original_language`, `id` và `tconst`. Bắt đầu với tác phẩm `Released`, phát hành 1990–2024, có `budget > 0`, `revenue > 0`, có thể loại và cả hai mã xuất hiện đúng một lần trong raw. Kiểm tra sơ bộ ngày 17/11/2026 có **8.049 bản ghi** đáp ứng các điều kiện này. Trước khi so sánh các giá trị tiền tệ, cần đối chiếu đơn vị, phạm vi doanh thu và cách chuẩn hóa của nguồn.
- **D4** — Chia nhóm ngân sách trong từng giai đoạn phát hành rồi so sánh phân phối và trung vị doanh thu giữa các thể loại có đủ mẫu. Đối chiếu thêm thành phần ngôn ngữ gốc để xem các nhóm so sánh có khác nhau rõ rệt về yếu tố này không. Chọn ranh giới nhóm và phạm vi so sánh sau khi kiểm tra phân phối cùng số mẫu.
- **D5** — Ước lượng khoảng tin cậy 95% cho trung vị doanh thu và chênh lệch giữa các thể loại trong những nhóm so sánh bằng bootstrap theo tác phẩm. Giữ các nhãn thể loại đi cùng tác phẩm khi lấy mẫu lại.
- **D6** — Kiểm tra kết luận khi thay đổi cách chia nhóm ngân sách và khi xử lý các giá trị tài chính cực trị theo một quy tắc đã giải thích. Báo cáo số mẫu sau từng lựa chọn.
- **Cách trình bày dự kiến** — Một biểu đồ ngân sách–doanh thu để giới thiệu phạm vi dữ liệu, một biểu đồ so sánh doanh thu giữa các thể loại trong cùng nhóm ngân sách và giai đoạn. Ghi rõ đơn vị đã xác minh, số mẫu và độ bất định.
- **Giới hạn cần giải thích** — Thông tin tài chính dương chỉ có ở một phần nhỏ dữ liệu. Mẫu sơ bộ có **72,68%** tác phẩm ngôn ngữ gốc `en`, nên kết quả cần được diễn giải trong phạm vi mẫu có thông tin tài chính. Doanh thu, ngân sách và lợi nhuận là các đại lượng khác nhau. Dataset còn thiếu những khoản chi phí và phân chia doanh thu cần để đánh giá lợi nhuận thực. Khi một tác phẩm thuộc nhiều thể loại, so sánh các phân phối theo nhóm và báo cáo số tác phẩm riêng biệt, đồng thời xác định cách phân bổ trước khi tính tổng doanh thu.

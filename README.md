# TMDB + IMDb Movies Dataset

Dự án cuối kỳ môn **Lập trình cho khoa học dữ liệu**, sử dụng dữ liệu phim kết hợp từ TMDB và IMDb để khám phá mối liên hệ giữa ngân sách, doanh thu, đặc điểm phim và đánh giá của khán giả.

## 1. Giới thiệu dataset

Nhóm sử dụng **TMDB + IMDB Merged Movies Dataset**, được tài khoản **ggtejas** công bố trên [Kaggle](https://www.kaggle.com/datasets/ggtejas/tmdb-imdb-merged-movies-dataset/data).

Theo mô tả của người đăng, bộ dữ liệu kết hợp metadata TMDB từ [dataset của asaniczka](https://www.kaggle.com/datasets/asaniczka/tmdb-movies-dataset-2023-930k-movies) với [IMDb Non-Commercial Datasets](https://developer.imdb.com/non-commercial-datasets/). File kết hợp bổ sung thông tin đạo diễn, biên kịch, diễn viên và đánh giá IMDb bên cạnh các thuộc tính TMDB.

| Đặc điểm | Nội dung |
| --- | --- |
| File sử dụng | `TMDB  IMDB Movies Dataset.csv` (hai dấu cách giữa TMDB và IMDB) |
| Quy mô bản CSV đang sử dụng | **443.656 bản ghi, 29 cột**, không tính dòng tiêu đề, trước khi làm sạch |
| Dung lượng | **282.010.663 byte**, khoảng **282,0 MB** (1 MB = 1.000.000 byte) |
| Ngày tải bản dữ liệu đang sử dụng | **05/11/2026** |
| Ý nghĩa mỗi dòng | Một bản ghi thông tin phim sau khi kết hợp hai nguồn; cần kiểm tra tính duy nhất của mã phim khi khám phá dữ liệu |
| Định dạng | CSV |
| Giấy phép công bố trên Kaggle | **CC BY-NC-SA 4.0** |

Số bản ghi, cột và dung lượng được kiểm tra trực tiếp trên bản CSV của nhóm ngày **05/11/2026**. Ngày tải thể hiện thời điểm nhóm lấy bản dữ liệu, không phải ngày cập nhật của toàn bộ dữ liệu trên TMDB/IMDb. Quy mô này đáp ứng điều kiện **hơn 10.000 mẫu và hơn 10 thuộc tính** ở dữ liệu đầu vào. Số bản ghi sử dụng cho từng câu hỏi sẽ được báo cáo riêng sau tiền xử lý.

## 2. Tải dữ liệu

**CSV có dung lượng lớn hơn 100 MB nên không được lưu trực tiếp trong repository này.** Nhóm cung cấp file qua Google Drive. Khi clone repo, cần tải CSV riêng trước khi chạy notebook.

- **[Tải CSV từ Google Drive](https://drive.google.com/file/d/1g1Wy1l1x1INs0JDn8SZuHJy1GsFj5O8D/view?usp=sharing)** — bản dữ liệu nhóm tải ngày **05/11/2026** để thực hiện đồ án.
- **[Trang nguồn trên Kaggle](https://www.kaggle.com/datasets/ggtejas/tmdb-imdb-merged-movies-dataset/data)** — mô tả dataset, nguồn gốc và giấy phép.

Tải file về, đặt cùng thư mục với `README.md` và giữ tên `TMDB  IMDB Movies Dataset.csv`. Nếu tên file tải về khác, đổi tên cho khớp hoặc sửa đường dẫn khi đọc dữ liệu. CSV này đã được thêm vào `.gitignore` để tránh đưa file lớn lên GitHub.

```python
import pandas as pd

movies = pd.read_csv("TMDB  IMDB Movies Dataset.csv", low_memory=False)
print(movies.shape)
movies.head()
```

Với máy có bộ nhớ hạn chế, có thể đọc các cột cần dùng bằng `usecols` hoặc đọc theo từng phần bằng `chunksize`. Chỉ cần tải file kết hợp ở trên để thực hiện đồ án.

## 3. Giấy phép và mục đích sử dụng

Kaggle công bố bộ dữ liệu dưới giấy phép **[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)**. Theo giấy phép công bố, dữ liệu có thể được sử dụng, chia sẻ và xử lý cho **mục đích học tập, nghiên cứu phi thương mại**, với các điều kiện:

- **Ghi công:** dẫn nguồn dataset, người công bố, giấy phép và nêu rõ các thay đổi nếu có.
- **Phi thương mại:** không sử dụng cho mục đích thương mại.
- **Chia sẻ tương tự:** nếu phân phối bản dữ liệu đã chỉnh sửa, áp dụng cùng giấy phép hoặc giấy phép tương thích theo điều khoản CC.

Nguồn trích dẫn: **ggtejas, TMDB + IMDB Merged Movies Dataset, Kaggle**; dữ liệu TMDB do **asaniczka** cung cấp trên Kaggle và dữ liệu IMDb từ **IMDb Non-Commercial Datasets**. Nhóm sử dụng file tải về làm dữ liệu đầu vào; các thay đổi khi làm sạch sẽ được mô tả trong notebook.

Do dữ liệu được kết hợp từ nhiều nguồn, cần đồng thời lưu ý [điều kiện sử dụng dữ liệu IMDb](https://developer.imdb.com/non-commercial-datasets/) và [TMDB](https://developer.themoviedb.org/docs/faq). Nhãn giấy phép của bản tổng hợp không thay thế các điều kiện của nguồn gốc. Đồ án sử dụng dữ liệu cho phân tích học thuật phi thương mại và ghi rõ nguồn.

## 4. Các thuộc tính chính

| Cột | Ý nghĩa |
| --- | --- |
| `id`, `tconst` | Mã định danh TMDB và IMDb |
| `title`, `original_title` | Tên phim và tên gốc |
| `budget`, `revenue` | Ngân sách sản xuất và doanh thu được ghi nhận |
| `vote_average`, `vote_count` | Điểm trung bình và số lượt đánh giá trên TMDB |
| `averageRating`, `numVotes` | Điểm đánh giá và số lượt đánh giá trên IMDb |
| `release_date`, `runtime`, `status` | Ngày phát hành, thời lượng và trạng thái phim |
| `genres`, `keywords` | Thể loại và từ khóa |
| `directors`, `writers`, `cast` | Đạo diễn, biên kịch và diễn viên |
| `production_companies`, `production_countries` | Công ty và quốc gia sản xuất |
| `original_language`, `spoken_languages` | Ngôn ngữ gốc và các ngôn ngữ sử dụng |
| `overview`, `tagline` | Tóm tắt và câu giới thiệu phim |
| `popularity`, `adult` | Chỉ số phổ biến TMDB và cờ nội dung người lớn |
| `homepage`, `poster_path`, `backdrop_path` | Trang chủ và đường dẫn hình ảnh |

## 5. Lý do lựa chọn và sự phù hợp với đồ án

Chủ đề phim ảnh gần gũi và có nhiều câu hỏi thực tế để khám phá. Bộ dữ liệu có đủ quy mô yêu cầu, nhiều loại thuộc tính và đánh giá từ hai nền tảng, giúp nhóm nghiên cứu cả doanh thu lẫn sự đón nhận của khán giả. Các thông tin về thể loại, thời gian phát hành và người tham gia sản xuất còn hỗ trợ phân tích theo nhóm.

Đối chiếu với yêu cầu **Final Project.pdf** và điều kiện quy mô của môn học:

| Yêu cầu | Cách triển khai với dataset |
| --- | --- |
| Dữ liệu công khai, nêu nguồn, cách thu thập và giấy phép | Dẫn trang Kaggle, mô tả việc kết hợp TMDB/IMDb và trình bày điều kiện sử dụng |
| Hơn 10.000 mẫu, hơn 10 thuộc tính | Bản CSV đang sử dụng có 443.656 bản ghi và 29 cột trước tiền xử lý |
| Khám phá cấu trúc, kiểu dữ liệu, phân phối, giá trị thiếu và trùng | Kiểm tra mã phim, chuyển kiểu ngày/số, khảo sát biến tài chính, đánh giá và biến phân loại |
| Đặt câu hỏi có ý nghĩa, cần nhiều bước để trả lời | Kết hợp lọc mẫu, tạo biến, phân nhóm, so sánh và trực quan hóa |
| Tiền xử lý và phân tích bằng mô tả lẫn code | Trình bày lý do chọn cách xử lý và số mẫu còn lại cho từng câu hỏi trong notebook |
| Reflection và references | Tổng kết khó khăn, bài học và tài liệu tham khảo sau khi thực hiện |
| Hợp tác bằng Git/GitHub | Quản lý notebook và tài liệu trên repo; các thành viên làm trên nhánh riêng và hợp nhất theo quy trình của đề |

README giới thiệu dữ liệu và định hướng; các kết quả phân tích sẽ được trình bày trong notebook sau khi thực hiện.

## 6. Câu hỏi phân tích dự kiến

| Câu hỏi | Ý nghĩa và hướng thực hiện |
| --- | --- |
| Ngân sách có mối liên hệ thế nào với doanh thu và đánh giá khán giả? Mối liên hệ có khác theo thể loại hoặc giai đoạn không? | Xét các khía cạnh của sự thành công, lọc mẫu có dữ liệu phù hợp, phân nhóm và so sánh; không suy diễn tương quan thành quan hệ nhân quả |
| Điểm TMDB và IMDb khác nhau như thế nào, và sự khác biệt có liên quan đến số lượt đánh giá hoặc thể loại không? | So sánh đánh giá giữa hai nền tảng trên cùng phim, xét ngưỡng số lượt chấm và độ ổn định của kết quả |
| Cơ cấu thể loại và thời lượng phim thay đổi ra sao qua các giai đoạn? | Chuẩn hóa ngày, tạo biến thời gian, xử lý phim nhiều thể loại rồi so sánh phân phối |
| Doanh thu và đánh giá khác nhau thế nào giữa các nhóm công ty sản xuất hoặc đạo diễn? | Chọn nhóm có đủ số phim, so sánh trong phạm vi ngân sách và giai đoạn tương đồng, tránh kết luận từ nhóm quá nhỏ |

Nhóm sẽ điều chỉnh để có **ít nhất số câu hỏi bằng số thành viên**, ưu tiên chất lượng và ý nghĩa phân tích.

### Các điểm cần kiểm tra trước phân tích

- Kiểm tra trùng toàn bộ bản ghi và trùng `id`/`tconst`, đặc biệt do dữ liệu được kết hợp từ hai nguồn.
- Kiểm tra giá trị thiếu, kiểu dữ liệu và giá trị bất thường. Không mặc định ngân sách hoặc doanh thu bằng 0 là giá trị thực.
- Xử lý các cột chứa nhiều giá trị theo định dạng thực tế; tránh đếm lặp phim/doanh thu khi tách thể loại.
- Xét điểm đánh giá cùng số lượt chấm của từng nền tảng; không trộn lẫn các cặp cột TMDB và IMDb.
- Với phân tích tài chính, báo cáo số mẫu hợp lệ, phạm vi kết luận và ảnh hưởng của thời gian/lạm phát. Tỷ lệ doanh thu/ngân sách chưa phản ánh lợi nhuận thực vì thiếu các chi phí và khoản phân chia doanh thu khác.

## 7. Tổ chức làm việc

Notebook dự kiến gồm: thu thập dữ liệu, khám phá dữ liệu, đặt câu hỏi, tiền xử lý và phân tích từng câu hỏi, reflection, references. Các thành viên cần có đóng góp trên nhánh riêng và hiểu phần việc của nhau.

**Liên kết kế hoạch nhóm:** Chưa có; sẽ bổ sung Google Sheets/Trello khi nhóm thống nhất phân công, nhiệm vụ và thời gian.

## Tài liệu tham khảo

- [ggtejas — TMDB + IMDB Merged Movies Dataset](https://www.kaggle.com/datasets/ggtejas/tmdb-imdb-merged-movies-dataset/data).
- [asaniczka — bộ dữ liệu TMDB nguồn](https://www.kaggle.com/datasets/asaniczka/tmdb-movies-dataset-2023-930k-movies).
- [IMDb Non-Commercial Datasets](https://developer.imdb.com/non-commercial-datasets/).
- [TMDB API FAQ](https://developer.themoviedb.org/docs/faq).
- [Creative Commons CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
- **Final Project.pdf** — tài liệu yêu cầu đồ án do giảng viên cung cấp.

# Movies Dataset

Repository giới thiệu bộ dữ liệu được chọn cho đồ án cuối kỳ môn **Lập trình cho khoa học dữ liệu**. Đề tài tập trung vào việc khám phá mối liên hệ giữa đặc điểm của phim, ngân sách, doanh thu và đánh giá của khán giả.

## 1. Giới thiệu dữ liệu

Dự án sử dụng file [`movies_metadata.csv`](movies_metadata.csv) thuộc **The Movies Dataset**, do **Rounak Banik** công bố trên [Kaggle, mục movies_metadata.csv](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset/data?select=movies_metadata.csv). Theo mô tả của tác giả, thông tin phim được thu thập qua TMDB API; bộ dữ liệu tổng thể còn kết hợp dữ liệu liên kết và đánh giá từ GroupLens/MovieLens.

Phạm vi hiện tại chỉ sử dụng **metadata của phim**, chưa sử dụng các file diễn viên, đoàn làm phim hay lịch sử chấm điểm của từng người dùng trong bộ dữ liệu đầy đủ.

| Đặc điểm | Nội dung |
| --- | --- |
| File sử dụng | `movies_metadata.csv` |
| Quy mô file thực tế | **45.466 dòng, 24 cột**, trước khi làm sạch |
| Ý nghĩa mỗi dòng | Một bản ghi thông tin phim; có bản ghi trùng nên số dòng chưa phải số phim duy nhất |
| Định dạng | CSV, dung lượng khoảng 34,4 MB |
| Nguồn metadata | The Movie Database (TMDB) |
| Giấy phép được ghi trên Kaggle | **CC0: Public Domain** |

### Giấy phép và mục đích sử dụng

Trang công bố trên [Kaggle](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset) ghi **CC0: Public Domain**. Theo [Creative Commons CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/), người dùng được sao chép, chỉnh sửa và phân phối tác phẩm thuộc phạm vi CC0 mà không cần xin phép, kể cả cho mục đích thương mại. **Vì vậy, theo giấy phép do tác giả công bố, bộ dữ liệu phù hợp để sử dụng cho mục đích học tập, nghiên cứu và phân tích trong đồ án này.**

Nhóm vẫn ghi rõ tác giả, nguồn Kaggle và nguồn metadata TMDB để bảo đảm khả năng truy xuất và trích dẫn học thuật. CC0 không bảo đảm dữ liệu chính xác hoặc sạch hoàn toàn, và không tự động xóa bỏ các quyền của bên thứ ba. Phạm vi đồ án là phân tích file metadata; nhãn giấy phép này không được dùng để suy rộng quyền sử dụng mọi ảnh poster hoặc nội dung bên ngoài được liên kết trong file.

### Đối chiếu file với nguồn

Ngày **11/10/2026**, file trong repository đã được so sánh với `movies_metadata.csv` tải trực tiếp từ Kaggle: **hai file khớp hoàn toàn từng byte**, cùng mã SHA-256:

```text
37ec322786b136a24604564e55160be75f8937546f11cb1a990076971fa895fd
```

Các bản ghi trùng và dòng bất thường được nêu bên dưới cũng xuất hiện trong bản tải từ Kaggle. Đây là đặc điểm của dữ liệu nguồn tại thời điểm kiểm tra, không phải lỗi phát sinh do tải file. File CSV gốc được giữ nguyên; các bước làm sạch sẽ được thực hiện và giải thích trong notebook.

### Các thuộc tính

| Cột | Ý nghĩa |
| --- | --- |
| `id`, `imdb_id` | Mã định danh phim trên TMDB và IMDb |
| `title`, `original_title` | Tên phim và tên gốc |
| `overview`, `tagline` | Tóm tắt nội dung và câu giới thiệu phim |
| `genres` | Danh sách thể loại |
| `belongs_to_collection` | Thông tin bộ sưu tập/loạt phim mà phim thuộc về, nếu có |
| `budget`, `revenue` | Ngân sách sản xuất và doanh thu được ghi nhận |
| `release_date`, `runtime` | Ngày phát hành và thời lượng phim tính bằng phút |
| `original_language`, `spoken_languages` | Ngôn ngữ gốc và các ngôn ngữ được sử dụng |
| `production_companies`, `production_countries` | Các công ty và quốc gia sản xuất |
| `popularity` | Chỉ số độ phổ biến do TMDB cung cấp |
| `vote_average`, `vote_count` | Điểm đánh giá trung bình và số lượt đánh giá trên TMDB |
| `status` | Trạng thái phát hành/sản xuất |
| `adult`, `video` | Các cờ đánh dấu nội dung người lớn và video trong metadata |
| `homepage`, `poster_path` | Trang chủ và đường dẫn ảnh poster |

## 2. Vì sao chọn bộ dữ liệu này?

- **Chủ đề gần gũi, dễ đặt câu hỏi có ý nghĩa.** Phim ảnh cho phép tìm hiểu các vấn đề như phim có ngân sách cao có doanh thu tốt hơn không, hay phim được chấm điểm cao có đồng thời thu hút nhiều lượt đánh giá không.
- **Có nhiều loại dữ liệu để thực hành.** File chứa dữ liệu số, phân loại, ngày tháng, văn bản và danh sách được lưu dưới dạng chuỗi. Nhờ đó, có thể luyện tập đọc dữ liệu, chuyển kiểu, tách thông tin và trực quan hóa bằng Python.
- **Có những vấn đề dữ liệu thực tế cần xử lý.** Dữ liệu chưa được làm sạch hoàn toàn, tạo cơ hội giải thích và lựa chọn cách xử lý thay vì chỉ vẽ biểu đồ trên dữ liệu đã chuẩn bị sẵn.
- **Quy mô phù hợp với đồ án.** Hơn 45 nghìn bản ghi đủ để so sánh nhiều nhóm phim, trong khi một file CSV khoảng 34,4 MB vẫn thuận tiện để xử lý bằng pandas và Jupyter Notebook.
- **Hỗ trợ nhiều hướng phân tích liên quan với nhau.** Các thuộc tính về thể loại, thời gian, ngân sách và đánh giá giúp xây dựng một câu chuyện phân tích thống nhất, đồng thời có thể chia câu hỏi cho các thành viên.

## 3. Mức độ phù hợp với yêu cầu Final Project

Đối chiếu với tài liệu **Final Project.pdf** của môn học:

| Yêu cầu trong đề bài | Cách bộ dữ liệu hỗ trợ |
| --- | --- |
| Chọn dữ liệu công khai; nêu chủ đề, nguồn, giấy phép và cách thu thập | Có trang công bố trên Kaggle, tác giả, giấy phép CC0 phù hợp cho học tập/nghiên cứu và mô tả nguồn TMDB/GroupLens |
| Khám phá số dòng/cột, ý nghĩa bản ghi, kiểu dữ liệu và dữ liệu trùng | File gồm 45.466 dòng, 24 cột với nhiều kiểu thuộc tính; cần kiểm tra trùng cả theo toàn bộ dòng và mã phim |
| Khảo sát phân phối, giá trị thiếu và bất thường của biến số/phân loại | Có thể phân tích ngân sách, doanh thu, thời lượng, điểm đánh giá, thể loại và ngôn ngữ |
| Đặt câu hỏi có ý nghĩa, cần nhiều bước để trả lời | Có thể kết hợp lọc dữ liệu, tạo biến, phân nhóm và trực quan hóa để nghiên cứu các mối liên hệ |
| Tiền xử lý và phân tích từng câu hỏi bằng mô tả lẫn code | Cần chuyển kiểu số/ngày, xử lý giá trị thiếu, giải mã danh sách và chọn tập dữ liệu phù hợp cho từng câu hỏi |
| Trình bày trong Jupyter Notebook, có reflection và references | Có thể tổ chức notebook theo các bước của đề bài; bổ sung nhận xét, khó khăn và tài liệu tham khảo sau khi thực hiện |
| Làm việc nhóm bằng Git/GitHub | Repo là nơi quản lý dữ liệu, notebook và lịch sử đóng góp; các thành viên làm trên nhánh riêng và hợp nhất theo quy trình của đề |

**Bộ dữ liệu phù hợp để triển khai đồ án, nhưng README này mới giới thiệu lựa chọn dữ liệu và định hướng.** Phần phân tích, notebook và minh chứng làm việc nhóm cần được thực hiện ở các bước tiếp theo.

### Những điểm cần tiền xử lý

Kiểm tra sơ bộ trực tiếp trên file CSV bằng pandas cho thấy:

- Có **17 bản ghi dư do trùng hoàn toàn cả 24 cột với bản ghi đã xuất hiện trước đó**, theo `movies.duplicated().sum()`, chiếm khoảng **0,037%** tổng số dòng. Ví dụ, có bản ghi lặp của *The Promise* (`id=105045`) và *Le Samouraï* (`id=5511`). Con số 17 là số lần lặp dư, không phải số phim có cùng tên. Nếu chỉ bỏ các bản sao giống hoàn toàn bằng `drop_duplicates()`, dữ liệu còn **45.449 dòng**.
- Khi chỉ xét `id`, có **30 lần lặp sau lần xuất hiện đầu tiên**. Con số này **đã bao gồm** các dòng trùng hoàn toàn, không cộng thêm 17 thành 47. Những dòng cùng mã phim nhưng khác thuộc tính cần được đối chiếu trước khi chọn bản ghi giữ lại.
- `runtime` thiếu **263** giá trị, `overview` thiếu **954** giá trị và `release_date` thiếu **87** giá trị.
- Có **3 dòng có dấu hiệu lệch cột**, chiếm khoảng **0,0066%**: `id` chứa ngày tháng, `budget` chứa đường dẫn ảnh `.jpg`, còn `title` bị thiếu. Chúng nằm tại index pandas **19730, 29503 và 35587** (đếm từ 0, không phải số dòng văn bản trong CSV). Cần kiểm tra riêng; nếu không khôi phục được đáng tin cậy thì loại khỏi tập phân tích và ghi rõ lý do, không tự đoán giá trị thay thế.
- `budget` có **36.573** giá trị bằng 0 và `revenue` có **38.052** giá trị bằng 0. Không nên mặc định chúng đều là ngân sách/doanh thu thực bằng 0; khi phân tích tài chính cần nêu rõ cách xử lý và số bản ghi còn lại.
- Các cột như `genres`, `production_companies` và `spoken_languages` lưu danh sách dưới dạng chuỗi, cần chuyển đổi trước khi phân nhóm.

Với ngày phát hành, cần kiểm tra giá trị hợp lệ và mốc thời gian phân tích. Điểm đánh giá phải được xem cùng số lượt đánh giá; các kết quả trên tập phim có đủ ngân sách/doanh thu có thể không đại diện cho toàn bộ dữ liệu.

**Đánh giá mức độ phù hợp:** Bản ghi trùng, giá trị thiếu và lỗi kiểu dữ liệu là những vấn đề thường gặp khi làm việc với dữ liệu thực tế. Số bản ghi trùng hoàn toàn và số dòng lệch cột ở đây rất nhỏ, có thể xử lý minh bạch và không phải lý do để loại bỏ toàn bộ dataset. Chúng cũng phù hợp với yêu cầu khám phá và tiền xử lý trong đề bài. Hạn chế đáng chú ý hơn là độ đầy đủ của dữ liệu tài chính: trên file gốc, chỉ **5.381 dòng có cả `budget > 0` và `revenue > 0`**, trước khi xử lý trùng và các vấn đề khác. Vì vậy, câu hỏi về ngân sách/doanh thu cần báo cáo số mẫu còn lại và giới hạn kết luận; các câu hỏi về thể loại, thời lượng và đánh giá vẫn có thể sử dụng những tập bản ghi phù hợp riêng.

## 4. Câu hỏi phân tích dự kiến

Đây là các hướng đề xuất, chưa phải kết quả phân tích. Nhóm sẽ chọn và điều chỉnh để có **ít nhất số câu hỏi bằng số thành viên**, đồng thời ưu tiên chất lượng theo yêu cầu đề bài.

| Câu hỏi | Ý nghĩa và hướng thực hiện |
| --- | --- |
| Mối liên hệ giữa ngân sách và doanh thu có khác nhau theo thể loại và giai đoạn phát hành không? | Tìm hiểu sự khác biệt giữa các nhóm phim. Lọc bản ghi có thông tin tài chính phù hợp, xử lý ngoại lệ, phân nhóm và so sánh tương quan; không suy diễn quan hệ nhân quả |
| Thứ hạng đánh giá của các thể loại thay đổi thế nào khi xét đến số lượt đánh giá? | Hạn chế kết luận từ phim có quá ít người chấm. Tách thể loại, thử các ngưỡng `vote_count`, so sánh phân phối điểm và độ ổn định của kết quả |
| Cơ cấu thể loại và thời lượng phim thay đổi như thế nào qua các thập niên trong bộ dữ liệu? | Mô tả xu hướng trong mẫu dữ liệu. Chuẩn hóa ngày, tạo biến thập niên, xử lý phim có nhiều thể loại và thời lượng bất thường trước khi tổng hợp |
| Phim thuộc bộ sưu tập/loạt phim có khác biệt về doanh thu và đánh giá so với các phim còn lại không? | Tìm hiểu đặc điểm của nhóm phim thuộc loạt. Tạo biến từ `belongs_to_collection`, so sánh trong các nhóm ngân sách và giai đoạn tương đồng, kèm quy mô mẫu |

Khi tách một phim thành nhiều thể loại, cần nêu rõ cách đếm để tránh cộng lặp tổng doanh thu hoặc số phim. Khi so sánh tiền tệ qua nhiều năm, cần xét ảnh hưởng của lạm phát hoặc giới hạn so sánh trong cùng giai đoạn. Doanh thu trừ ngân sách sản xuất chưa phản ánh đầy đủ lợi nhuận vì thiếu các chi phí khác.

## 5. Nội dung repository và bước tiếp theo

```text
Movies-Dataset/
├── README.md
└── movies_metadata.csv
```

Có thể đọc dữ liệu ban đầu bằng:

```python
import pandas as pd

movies = pd.read_csv("movies_metadata.csv", low_memory=False)
print(movies.shape)
movies.head()
```

Notebook sẽ được triển khai theo các mục: thu thập dữ liệu, khám phá dữ liệu, đặt câu hỏi, tiền xử lý và phân tích từng câu hỏi, reflection, references. Mỗi thành viên cần có đóng góp trên nhánh riêng và hiểu phần việc của các thành viên khác theo yêu cầu của đề.

**Liên kết kế hoạch nhóm:** Chưa có; sẽ bổ sung link Google Sheets/Trello khi nhóm lập kế hoạch phân công, thời gian và nhiệm vụ theo yêu cầu của đề bài.

## Tài liệu tham khảo

- Rounak Banik, [The Movies Dataset trên Kaggle](https://www.kaggle.com/datasets/rounakbanik/the-movies-dataset): nguồn dữ liệu, mô tả thu thập và giấy phép.
- Creative Commons, [CC0 1.0 Universal](https://creativecommons.org/publicdomain/zero/1.0/): giải thích quyền sao chép, chỉnh sửa và phân phối theo CC0.
- [The Movie Database (TMDB)](https://www.themoviedb.org/): nguồn metadata phim.
- [GroupLens MovieLens](https://grouplens.org/datasets/movielens/): nguồn MovieLens được tác giả sử dụng trong bộ dữ liệu tổng thể.
- **Final Project.pdf**, tài liệu yêu cầu đồ án do giảng viên cung cấp: phần Collecting data, Exploring data, Asking meaningful questions, Preprocessing + analyzing data, Reflection, References và Teamwork.

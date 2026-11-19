# TMDB + IMDb Movies Dataset

Dự án cuối kỳ môn **Lập trình cho khoa học dữ liệu**, sử dụng dữ liệu phim kết hợp từ TMDB và IMDb để khám phá mối liên hệ giữa ngân sách, doanh thu, đặc điểm phim và đánh giá của khán giả.

## 1. Giới thiệu dataset

Nhóm sử dụng **TMDB + IMDB Merged Movies Dataset**, được tài khoản **ggtejas** công bố trên [Kaggle](https://www.kaggle.com/datasets/ggtejas/tmdb-imdb-merged-movies-dataset/data).

Theo mô tả của người đăng, bộ dữ liệu kết hợp metadata TMDB từ [dataset của asaniczka](https://www.kaggle.com/datasets/asaniczka/tmdb-movies-dataset-2023-930k-movies) với [IMDb Non-Commercial Datasets](https://developer.imdb.com/non-commercial-datasets/). File kết hợp bổ sung thông tin đạo diễn, biên kịch, diễn viên và đánh giá IMDb bên cạnh các thuộc tính TMDB.

| Đặc điểm | Nội dung |
| --- | --- |
| File sử dụng | `data/raw/TMDB  IMDB Movies Dataset.csv` (hai dấu cách giữa TMDB và IMDB) |
| Quy mô bản CSV đang sử dụng | **443.656 bản ghi, 29 cột**, không tính dòng tiêu đề, trước khi làm sạch |
| Dung lượng | **282.010.663 byte**, khoảng **282,0 MB** (1 MB = 1.000.000 byte) |
| Ngày tải bản dữ liệu đang sử dụng | **05/11/2026** |
| Ý nghĩa mỗi dòng | Một bản ghi thông tin phim sau khi kết hợp hai nguồn; cần kiểm tra tính duy nhất của mã phim khi khám phá dữ liệu |
| Định dạng | CSV |
| Giấy phép công bố trên Kaggle | **CC BY-NC-SA 4.0** |

Số bản ghi, cột và dung lượng được kiểm tra trực tiếp trên bản CSV của nhóm ngày **05/11/2026**. Ngày tải thể hiện thời điểm nhóm lấy bản dữ liệu, không phải ngày cập nhật của toàn bộ dữ liệu trên TMDB/IMDb. Quy mô này đáp ứng điều kiện **tối thiểu khoảng 3.000 dòng và 10 cột** trong đề. Số bản ghi sử dụng cho từng câu hỏi sẽ được báo cáo riêng sau tiền xử lý.

## 2. Tải dữ liệu

**CSV có dung lượng lớn hơn 100 MB nên không được lưu trực tiếp trong repository này.** Nhóm cung cấp file qua Google Drive. Khi clone repo, cần tải CSV riêng trước khi chạy notebook.

- **[Tải CSV từ Google Drive](https://drive.google.com/file/d/1g1Wy1l1x1INs0JDn8SZuHJy1GsFj5O8D/view?usp=sharing)** — bản dữ liệu nhóm tải ngày **05/11/2026** để thực hiện đồ án.
- **[Trang nguồn trên Kaggle](https://www.kaggle.com/datasets/ggtejas/tmdb-imdb-merged-movies-dataset/data)** — mô tả dataset, nguồn gốc và giấy phép.

Tải file về, đặt trong `data/raw/` và giữ tên `TMDB  IMDB Movies Dataset.csv`. Nếu tên file tải về khác, đổi tên cho khớp hoặc sửa đường dẫn khi đọc dữ liệu. Dữ liệu trong `data/raw/` và `data/processed/` được Git ignore; chỉ các file `.gitkeep` được theo dõi để giữ cấu trúc thư mục. Giữ nguyên dữ liệu gốc trong `data/raw/`, lưu dữ liệu đã xử lý vào `data/processed/`.

Ví dụ khi chạy từ thư mục gốc repository:

```python
import pandas as pd

movies = pd.read_csv("data/raw/TMDB  IMDB Movies Dataset.csv", low_memory=False)
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

Đối chiếu với [đề Final Project](doc/CSC17104_2026_Final_Project.pdf) và điều kiện quy mô của môn học:

| Yêu cầu | Cách triển khai với dataset |
| --- | --- |
| Dữ liệu công khai, nêu nguồn, cách thu thập và giấy phép | Dẫn trang Kaggle, mô tả việc kết hợp TMDB/IMDb và trình bày điều kiện sử dụng |
| Tối thiểu khoảng 3.000 dòng, 10 cột | Bản CSV đang sử dụng có 443.656 bản ghi và 29 cột trước tiền xử lý |
| Khám phá cấu trúc, kiểu dữ liệu, phân phối, giá trị thiếu và trùng | Kiểm tra mã phim, chuyển kiểu ngày/số, khảo sát biến tài chính, đánh giá và biến phân loại |
| Đặt câu hỏi có ý nghĩa, cần nhiều bước để trả lời | Kết hợp lọc mẫu, tạo biến, phân nhóm, so sánh và trực quan hóa |
| Tiền xử lý và phân tích bằng mô tả lẫn code | Trình bày lý do chọn cách xử lý và số mẫu còn lại cho từng câu hỏi trong notebook |
| Reflection và references | Tổng kết khó khăn, bài học và tài liệu tham khảo sau khi thực hiện |
| Hợp tác bằng Git/GitHub | Quản lý notebook và tài liệu trên repo; các thành viên làm trên nhánh riêng và hợp nhất theo quy trình của đề |

README giới thiệu dữ liệu và định hướng. Bốn câu hỏi đã được chốt trong [QUESTIONS.md](doc/QUESTIONS.md). [Notebook 01](notebooks/01_collection_exploration.ipynb) khám phá raw và các mẫu phục vụ từng câu hỏi.

## 6. Câu hỏi phân tích dự kiến

| Câu hỏi | Ý nghĩa và hướng thực hiện |
| --- | --- |
| Q1. IMDb và TMDB chấm điểm lệch nhau như thế nào? | Khang phụ trách. So sánh cặp điểm, xét thể loại và độ nhạy theo ngưỡng lượt chấm. |
| Q2. Nhìn hồ sơ phim, đoán khán giả IMDb chấm mấy điểm? | Khang phụ trách, dùng ML. Dự đoán từ thể loại, thời lượng, ngôn ngữ gốc và năm phát hành, với cách chia tập theo thời gian. |
| Q3. Phim có ngày càng dài hơn không? | Khánh phụ trách. So sánh thời lượng qua các giai đoạn, kiểm tra trong các nhóm thể loại và ngôn ngữ. |
| Q4. Cùng mức ngân sách, thể loại phim nào thường có doanh thu cao hơn? | Khánh phụ trách. So sánh các nhóm có ngân sách, giai đoạn tương đồng sau khi xác minh thông tin tài chính của nguồn. |

Động cơ, phạm vi dữ liệu, tiêu chí D và giới hạn của từng câu được ghi trong [QUESTIONS.md](doc/QUESTIONS.md). Nhóm có **3 câu non-ML và 1 câu ML**, mỗi người phụ trách **2 câu**. Các câu non-ML dự kiến sử dụng D2–D6, với ít nhất hai tiêu chí cho mỗi câu. Câu ML thực hiện theo bộ yêu cầu riêng trong đề.

### Các điểm cần kiểm tra trước phân tích

- Kiểm tra trùng toàn bộ bản ghi và trùng `id`/`tconst`, đặc biệt do dữ liệu được kết hợp từ hai nguồn.
- Kiểm tra giá trị thiếu, kiểu dữ liệu và giá trị bất thường. Không mặc định ngân sách hoặc doanh thu bằng 0 là giá trị thực.
- Xử lý các cột chứa nhiều giá trị theo định dạng thực tế; tránh đếm lặp phim/doanh thu khi tách thể loại.
- Xét điểm đánh giá cùng số lượt chấm của từng nền tảng; không trộn lẫn các cặp cột TMDB và IMDb.
- Với phân tích tài chính, báo cáo số mẫu hợp lệ, phạm vi kết luận và ảnh hưởng của thời gian/lạm phát. Tỷ lệ doanh thu/ngân sách chưa phản ánh lợi nhuận thực vì thiếu các chi phí và khoản phân chia doanh thu khác.

## 7. Tổ chức làm việc

Các thành viên cần có đóng góp trên Git và hiểu toàn bộ bài làm để trả lời Q&A. Bổ sung tên, MSSV và phân công thực tế vào bảng sau:

| Thành viên | MSSV | Câu hỏi phụ trách | Công việc |
| --- | --- | --- | --- |
| Thành viên 1 — chưa điền | Chưa điền | Q1, Q2 (dự kiến) | Chưa phân công chi tiết |
| Thành viên 2 — chưa điền | Chưa điền | Q3, Q4 (dự kiến) | Chưa phân công chi tiết |

Xem [kế hoạch nhóm](doc/planning/PLAN.md) để theo dõi việc tiếp theo, phân công và bàn giao.

## 8. Cấu trúc repository và cách chạy

```text
MoviesDataset/
├── README.md
├── environment.yml
├── LLM_USAGE.md
├── data/
│   ├── raw/
│   │   └── TMDB  IMDB Movies Dataset.csv  # tải riêng, không commit
│   └── processed/                       # dữ liệu sau xử lý, không commit
├── src/                                 # các hàm Python dùng chung
│   └── __init__.py
├── notebooks/
│   └── 01_collection_exploration.ipynb   # đã chạy, có bảng và biểu đồ
└── doc/
    ├── CSC17104_2026_Final_Project.pdf
    └── planning/
        ├── PLAN.md
        └── data-exploration/
            └── task.md
```

Đã cập nhật [notebook thu thập và khám phá](notebooks/01_collection_exploration.ipynb) ngày **19/11/2026**, gồm **50 cell code đã chạy và 12 hình**. Các mục từ 2 đến 7 được chia nhỏ, có lời giải thích cạnh bảng/hình và thu gọn code mặc định. Notebook trình bày quy mô các mẫu khám phá, mối liên hệ sơ bộ giữa các thuộc tính và hướng tiền xử lý Q1–Q4. Phân tích chi tiết dự kiến thực hiện trong `02_analysis.ipynb` và `03_ml_question.ipynb`.

Notebook 01 tự tìm thư mục gốc repository, giữ nguyên CSV và lưu bảng/biểu đồ trong file `.ipynb`. Khi đã kích hoạt `movies-dataset`, có thể chạy lại toàn bộ bằng:

```bash
PYTHONNOUSERSITE=1 python -m nbconvert --to notebook --execute --inplace --ExecutePreprocessor.timeout=300 notebooks/01_collection_exploration.ipynb
```

`PYTHONNOUSERSITE=1` tránh nạp lẫn thư viện Python cài riêng ngoài Conda. Trên PowerShell, đặt `$env:PYTHONNOUSERSITE = '1'` trước rồi chạy lệnh `python -m nbconvert ...` tương tự. Khi mở JupyterLab, có thể dùng `PYTHONNOUSERSITE=1 python -m jupyterlab` và chọn kernel **Python (movies-dataset)**.

### Thiết lập Miniconda trên Ubuntu

Chạy mọi notebook, script Python và ví dụ Python của dự án trong môi trường Conda `movies-dataset` được khai báo ở `environment.yml`. Khi làm việc từ terminal, kích hoạt bằng `conda activate movies-dataset` trước khi chạy Python hoặc mở JupyterLab. Khi tạo hoặc mở notebook trong JupyterLab hay VS Code, chọn kernel **Python (movies-dataset)** trước khi chạy cell.

`environment.yml` ghim phiên bản Python và các thư viện trực tiếp theo nhóm chức năng, có chú thích cho từng package. Bộ thư viện phục vụ dữ liệu bảng, làm sạch, EDA, thống kê, hồi quy/phân loại, cross-validation, Pipeline và diễn giải mô hình. Các mô hình tuyến tính, cây, random forest và gradient boosting đã có trong scikit-learn.

Hai thành viên dùng **Miniconda trên Ubuntu**. Hướng dẫn chính dưới đây dành cho máy Intel/AMD 64-bit (`x86_64`), ví dụ Ubuntu 22.04/24.04. Miniconda có sẵn lệnh `conda`; không cần cài thêm Anaconda hoặc micromamba.

**1. Kiểm tra Miniconda và kiến trúc máy**

```bash
conda --version
uname -m
```

Nếu Bash chưa nhận lệnh `conda`, với Miniconda được cài ở vị trí mặc định:

```bash
source "$HOME/miniconda3/etc/profile.d/conda.sh"
conda init bash
```

Sau đó mở terminal mới. Nếu dùng thư mục cài khác, sửa đường dẫn tương ứng; nếu dùng Zsh, thay `bash` bằng `zsh`. Nếu chưa có Miniconda, xem [hướng dẫn cài trên Linux của Conda](https://docs.conda.io/projects/conda/en/stable/user-guide/install/linux.html).

**2. Mở repository**

Nếu chưa clone:

```bash
git clone https://github.com/tranthuankhang/Movies-Dataset.git MoviesDataset
cd MoviesDataset
```

Nếu đã clone, chỉ cần `cd` vào thư mục đang chứa `README.md` và `environment.yml`. Chạy các lệnh còn lại từ thư mục này.

**3. Tạo môi trường dùng chung — chỉ làm một lần trên mỗi máy**

Từ thư mục gốc repository, tạo môi trường bằng `environment.yml` nếu máy chưa có `movies-dataset`.

```bash
conda env create -f environment.yml
conda activate movies-dataset
```

Nếu đã có môi trường `movies-dataset`, chạy `conda activate movies-dataset` và kiểm tra phiên bản ở bước 5. YAML ghim 24 gói trực tiếp. Conda tự chọn các phụ thuộc gián tiếp và build phù hợp trên từng máy.

**4. Tải dữ liệu và đăng ký kernel**

Tải CSV từ link Google Drive ở mục 2. Đặt tại `data/raw/TMDB  IMDB Movies Dataset.csv` (hai dấu cách giữa TMDB và IMDB). Ví dụ file vừa tải nằm trong `~/Downloads`:

```bash
mkdir -p data/raw data/processed
mv "$HOME/Downloads/TMDB  IMDB Movies Dataset.csv" data/raw/
python -m ipykernel install --user --name movies-dataset --display-name "Python (movies-dataset)"
```

Nếu CSV đã nằm đúng chỗ thì bỏ qua lệnh `mv`; điều chỉnh đường dẫn Downloads nếu máy dùng vị trí tải khác.

**5. Kiểm tra môi trường và mở JupyterLab**

```bash
python --version
python -c "import numpy, pandas, scipy, sklearn, matplotlib, seaborn, statsmodels, pyarrow, imblearn; print('Import OK'); print('pandas:', pandas.__version__); print('scikit-learn:', sklearn.__version__)"
conda list
jupyter lab
```

Python cần là **3.11.13**, pandas **2.2.3** và scikit-learn **1.6.1**. Trong JupyterLab hoặc VS Code, chọn kernel **Python (movies-dataset)**. Ví dụ đọc dữ liệu ở mục 2 giả định thư mục làm việc là gốc repository; nếu chạy từ `notebooks/`, điều chỉnh đường dẫn về `../data/raw/`. Khi các notebook đã được nhóm viết, chạy theo thứ tự **01 → 02 → 03**.

**6. Những lần làm việc tiếp theo**

Mở terminal tại thư mục repository rồi chạy:

```bash
conda activate movies-dataset
jupyter lab
```

Kết thúc Jupyter bằng `Ctrl+C` trong terminal; thoát môi trường bằng `conda deactivate`.

Khi nhóm thống nhất đổi thư viện, cập nhật phiên bản trong `environment.yml` và dùng `conda env update -n movies-dataset -f environment.yml` để áp dụng trên mỗi máy. Dùng cùng bản CSV, quy tắc chia dữ liệu và giá trị `random_state` để kết quả có thể tái lập.

Trước khi nộp, nhóm bổ sung các câu hỏi đã chốt và người phụ trách, kết quả chính, các notebook công khai liên quan cùng điểm khác biệt của nhóm, reflection cá nhân và slides hoàn chỉnh. Duy trì nhật ký sử dụng LLM trong `LLM_USAGE.md`.

## Tài liệu tham khảo

- [ggtejas — TMDB + IMDB Merged Movies Dataset](https://www.kaggle.com/datasets/ggtejas/tmdb-imdb-merged-movies-dataset/data).
- [asaniczka — bộ dữ liệu TMDB nguồn](https://www.kaggle.com/datasets/asaniczka/tmdb-movies-dataset-2023-930k-movies).
- [IMDb Non-Commercial Datasets](https://developer.imdb.com/non-commercial-datasets/).
- [TMDB API FAQ](https://developer.themoviedb.org/docs/faq).
- [Creative Commons CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/).
- [Final Project](doc/CSC17104_2026_Final_Project.pdf) — tài liệu yêu cầu đồ án do giảng viên cung cấp.

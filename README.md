# Lab 03 - Trực quan hóa dữ liệu bằng Power BI

Repository của Nhóm 15 dùng để quản lý dữ liệu, file Power BI, báo cáo LaTeX và tài liệu phục vụ đồ án phân tích bộ dữ liệu **UK Road Safety / STATS19**.

## Thành viên

| Họ và tên | MSSV |
| :--- | :--- |
| Lê Lâm Trí Đức | `23120237` |
| Hoàng Quốc Việt | `23120189` |
| Nguyễn Lê Thế Vinh | `23120190` |
| Phạm Quang Vinh | `23120202` |

## Cấu trúc thư mục

```text
Lab03-Data-Visulization/
|-- data/
|   |-- raw/                 Dữ liệu STATS19 gốc, chưa xử lý
|   `-- processed/           Dữ liệu sạch dùng chung để phân tích
|-- powerbi/                 File Power BI nền, file cá nhân và dashboard tổng
|-- proposal_project/        Tài liệu đề xuất và lựa chọn dataset
|-- report/
|   |-- images/              Ảnh Data Model, biểu đồ và dashboard
|   |-- sections/            Nội dung từng mục của báo cáo LaTeX
|   |-- coverpage.tex        Trang bìa báo cáo
|   |-- main.tex             File LaTeX chính
|   `-- main.pdf             Báo cáo PDF sau khi build
|-- requirements/            Hình ảnh và tài liệu yêu cầu của bài thực hành
|-- video/                   File hoặc tài liệu phục vụ video thuyết trình
|-- assignment.md            Phân công công việc và lịch bàn giao
|-- project_approval_criteria.md
|                            Tiêu chí đánh giá và lựa chọn dataset
`-- README.md                Hướng dẫn sử dụng repository
```

## Chức năng các thư mục

### `data/`

- `data/raw/` chứa dữ liệu gốc tải từ nguồn chính thức. Không chỉnh sửa trực tiếp các file này.
- `data/processed/` chứa dữ liệu đã được làm sạch, chuẩn hóa và bàn giao cho cả nhóm.
  - *Lưu ý:* Việc làm sạch và tiền xử lý dữ liệu phải được thực hiện bằng công cụ **Power BI (Power Query)**, tuyệt đối không dùng các công cụ lập trình ngoài.
- Các file raw dung lượng lớn không được push lên GitHub.

### `powerbi/`

Chứa các file Power BI:

- File Power BI nền có Data Model và measure dùng chung.
- File phân tích cá nhân của từng thành viên:
  - `23120237_report.pbix`
  - `23120189_report.pbix`
  - `23120190_report.pbix`
  - `23120202_report.pbix`
- Dashboard tổng hợp: `group15_dashboard.pbix`.

### `report/`

- `main.tex` là điểm bắt đầu để build báo cáo.
- `sections/` chứa nội dung từng mục, giúp các thành viên chỉnh sửa độc lập.
- `images/` chứa ảnh chụp thực tế từ Power BI.
- `main.pdf` là bản PDF kết quả được phép push để cả nhóm kiểm tra.

Build báo cáo bằng lệnh:

```powershell
cd report
latexmk -xelatex -interaction=nonstopmode -halt-on-error main.tex
```

### `proposal_project/`

Chứa tài liệu giải thích quá trình đề xuất, so sánh và lựa chọn dataset STATS19.

### `requirements/`

Chứa ảnh chụp yêu cầu và tiêu chí của bài thực hành để nhóm đối chiếu khi hoàn thiện sản phẩm.

### `video/`

Chứa tài liệu, kịch bản hoặc file phục vụ quay video. Không push trực tiếp các file video dung lượng lớn lên GitHub.

## Quy trình làm việc

1. Đọc `assignment.md` để biết nhiệm vụ và hạn bàn giao.
2. Đồng bộ repository trước khi bắt đầu chỉnh sửa.
3. Chỉ sử dụng file Power BI nền và dữ liệu sạch đã được bàn giao.
4. Không tự ý thay đổi Data Model hoặc measure dùng chung.
5. Kiểm tra file thay đổi trước khi commit.
6. Commit với nội dung ngắn gọn, nêu rõ phần đã hoàn thành.

## Quy định Git và LaTeX

> **Không được push các file rác hoặc file tạm sinh ra khi build LaTeX lên GitHub.**

Các file không được commit gồm:

- `*.aux`
- `*.log`
- `*.toc`
- `*.lof`
- `*.lot`
- `*.out`
- `*.fls`
- `*.fdb_latexmk`
- `*.xdv`
- `*.synctex.gz`
- Thư mục `report/build/`

Các file này đã được khai báo trong `.gitignore`. Trước khi commit, bắt buộc chạy:

```powershell
git status
```

Chỉ commit mã nguồn LaTeX, ảnh cần thiết và `report/main.pdf`. Nếu thấy file build tạm xuất hiện trong danh sách chuẩn bị commit, phải loại file đó khỏi commit trước khi push.

## Quy định dữ liệu và file dung lượng lớn

- Không push dữ liệu raw dạng CSV, Excel, ZIP hoặc JSON lên GitHub.
- Không push file video `.mp4`, `.avi` hoặc `.mov` lên GitHub.
- Kiểm tra dung lượng file `.pbix` trước khi push; sử dụng phương thức chia sẻ ngoài GitHub nếu file vượt giới hạn.
- Không xóa hoặc chỉnh sửa file của thành viên khác khi chưa trao đổi.

## Sản phẩm cuối cùng

- Bộ dữ liệu sạch và Data Model dùng chung.
- Bốn file Power BI phân tích cá nhân.
- Một file dashboard tổng hợp.
- Báo cáo PDF không vượt quá 24 trang.
- Video thuyết trình hoàn chỉnh.

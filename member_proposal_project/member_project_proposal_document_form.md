# PHIẾU ĐỀ XUẤT BỘ DỮ LIỆU ĐỒ ÁN
## Đồ án Lab 03: Trực quan hóa dữ liệu bằng Power BI

*Thành viên nhóm điền đầy đủ các thông tin dưới đây để đề xuất bộ dữ liệu nghiên cứu.*

---

## 1. Thông tin thành viên đề xuất
-   **Họ và Tên**: ..............................................................
-   **MSSV**: ...................................................................
-   **Vai trò trong nhóm**: ......................................................

---

## 2. Thông tin chung về Bộ dữ liệu (Dataset Overview)
-   **Tên bộ dữ liệu**: ..........................................................
-   **Lĩnh vực/Chủ đề phân tích**: ................................................
-   **Nguồn cung cấp (Đường dẫn tải/Link)**: .......................................
-   **Định dạng tệp tin (CSV, XLSX, JSON...)**: ...................................
-   **Tổng dung lượng & Số lượng dòng**: .........................................

---

## 3. Cấu trúc Mô hình Quan hệ Đề xuất

### 3.1. Danh sách các bảng dữ liệu
*Liệt kê danh sách các bảng kèm theo số lượng dòng và vai trò (Fact hay Dimension).*

| Tên Bảng | Số lượng dòng | Vai trò (Fact / Dimension) | Ý nghĩa của bảng |
| :--- | :--- | :--- | :--- |
| **Bảng 1 (Fact)** | ................. | Fact Table | .................................................. |
| **Bảng 2 (Dim)** | ................. | Dimension Table | .................................................. |
| **Bảng 3 (Dim)** | ................. | Dimension Table | .................................................. |
| *Bảng 4 (nếu có)* | ................. | Dimension Table | .................................................. |

### 3.2. Dự kiến sơ đồ liên kết giữa các bảng (Schema Keys)
*Mô tả cách các bảng liên kết với nhau qua các khóa:*
-   Liên kết 1: Bảng **[Tên Bảng A]** liên kết với Bảng **[Tên Bảng B]** qua khóa ngoại `[Tên Trường Khóa]` (Quan hệ $1:\infty$).
-   Liên kết 2: Bảng **[Tên Bảng C]** liên kết với Bảng **[Tên Bảng D]** qua khóa ngoại `[Tên Trường Khóa]` (Quan hệ $1:\infty$).
-   *Các liên kết khác (nếu có):* ..................................................................................

---

## 4. Bảng tự đánh giá tiêu chí phê duyệt (Feasibility Checklist)
*Đánh dấu `[x]` vào các tiêu chí bộ dữ liệu đạt được:*

- [ ] **Tính quan hệ**: Có từ 2-3 bảng trở lên và thiết lập được quan hệ 1-nhiều rõ ràng (không phải bảng phẳng đơn lẻ).
- [ ] **Độ lớn dữ liệu**: Bảng Fact chính có trên 1,000 dòng dữ liệu thực tế.
- [ ] **Chiều thời gian**: Có chứa cột Ngày/Tháng/Năm (Date) để phân tích xu hướng.
- [ ] **Số đo lường**: Có ít nhất 2-3 cột số liệu định lượng (Sales, Quantity, Duration, Cost...).
- [ ] **Khả năng làm sạch**: Dữ liệu có thể xử lý và làm sạch bằng các công cụ cơ bản của Power Query.
- [ ] **Bảo mật**: Dữ liệu không chứa các thông tin cá nhân nhạy cảm thực tế (PII).

---

## 5. Phác thảo 4 Mục tiêu phân tích dự kiến cho nhóm

*Mô tả sơ bộ cách bộ dữ liệu này đáp ứng 4 góc nhìn phân tích tổng quan cho 4 thành viên:*

1.  **Mục tiêu 1 (Thành viên A - Thời gian & Chỉ số vĩ mô)**:
    -   *Các cột dữ liệu sử dụng*: ................................................................
    -   *Câu hỏi phân tích dự kiến*: ...............................................................
2.  **Mục tiêu 2 (Thành viên B - Phân loại & Danh mục)**:
    -   *Các cột dữ liệu sử dụng*: ................................................................
    -   *Câu hỏi phân tích dự kiến*: ...............................................................
3.  **Mục tiêu 3 (Thành viên C - Phân khúc & Hành vi Chủ thể)**:
    -   *Các cột dữ liệu sử dụng*: ................................................................
    -   *Câu hỏi phân tích dự kiến*: ...............................................................
4.  **Mục tiêu 4 (Thành viên D - Tương quan & Hiệu quả Vận hành)**:
    -   *Các cột dữ liệu sử dụng*: ................................................................
    -   *Câu hỏi phân tích dự kiến*: ...............................................................

---

## 6. Thách thức dự kiến & Các bước xử lý trên Power Query
-   **Thách thức của dữ liệu (Ví dụ: nhiều ô trống, sai lệch định dạng, cần gom nhóm...)**:
    ..........................................................................................................
-   **Dự kiến các bước tiền xử lý chính cần thực hiện**:
    ..........................................................................................................

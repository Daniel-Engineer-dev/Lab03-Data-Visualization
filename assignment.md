# BẢNG PHÂN CHIA CÔNG VIỆC - NHÓM XX
## Đồ án Lab 03: Trực quan hóa dữ liệu bằng Power BI (Khung Phân Công Tổng Quan)

Tài liệu này dùng để phân công nhiệm vụ tổng quan cho 4 thành viên trong nhóm nhằm hoàn thành đồ án trong vòng 14 ngày. Kế hoạch này được thiết kế tổng quát để có thể áp dụng cho **bất kỳ chủ đề hoặc bộ dữ liệu nào** mà nhóm lựa chọn.

---

## 1. Thông tin thành viên nhóm

| STT | Họ và Tên | MSSV | Vai trò chính | Tỷ lệ đóng góp (Dự kiến) |
| :--- | :--- | :--- | :--- | :--- |
| 1 | **Thành viên A** | `MSSV_A` | Trưởng nhóm, Data Modeler, Lead Dashboard Designer | 25% |
| 2 | **Thành viên B** | `MSSV_B` | PBI Researcher, Data Preparation Specialist | 25% |
| 3 | **Thành viên C** | `MSSV_C` | Interaction Developer, Report Writer | 25% |
| 4 | **Thành viên D** | `MSSV_D` | LaTeX Specialist, Video Editor | 25% |

*Lưu ý: Cả 4 thành viên đều tham gia trực tiếp vào việc phân tích dữ liệu và thiết lập các biểu đồ/chức năng trực quan hóa trên Power BI tương ứng với mục tiêu được phân công.*

---

## 2. Phân chia công việc chi tiết theo Thành viên

### 👤 Thành viên A (Trưởng nhóm)
*   **Nhiệm vụ chung**: Điều phối tiến độ, thiết kế mô hình dữ liệu chính (Data Model - thiết lập các liên kết) và thiết kế layout Dashboard tổng hợp (Storyboard).
*   **Mục tiêu phân tích riêng (Mục tiêu 1) - Phân tích Xu hướng Thời gian & Các KPI vĩ mô**:
    *   *Nội dung*: Tìm hiểu sự biến động của các chỉ số đo lường chính (Key Performance Indicators - KPIs) theo chiều thời gian (năm, quý, tháng, tuần) để xác định tính chu kỳ, xu hướng tăng trưởng hoặc suy thoái tổng thể.
    *   *Biểu đồ phụ trách*: Biểu đồ đường (Line Chart), biểu đồ cột (Column Chart), hoặc thẻ thông tin (KPI Card) tổng hợp chỉ số chính.
*   **Tiến trình công việc chi tiết**:
    *   **Ngày 1 - 3**: Họp nhóm chọn đề tài & dataset; tổng hợp cấu trúc dự án; viết phần giới thiệu chung.
    *   **Ngày 4 - 5**: Nhận dữ liệu đã làm sạch để thiết lập các mối quan hệ (Relationships) giữa các bảng trong Power BI (Star Schema / Snowflake Schema).
    *   **Ngày 6 - 9**: Thực hiện phân tích Mục tiêu 1 trên Power BI. Viết phần báo cáo cho mục tiêu này.
    *   **Ngày 8 - 9**: Ráp nối các biểu đồ của các thành viên thành Dashboard chung, thiết kế layout và luồng thông tin (Storyboard).
    *   **Ngày 10 - 12**: Chụp ảnh dashboard tổng thể, viết nhận xét chung và kết luận cho báo cáo. Hỗ trợ tổng hợp báo cáo.
    *   **Ngày 13 - 14**: Soạn kịch bản thuyết trình, cùng nhóm quay video demo dashboard và nén file nộp bài.

### 👤 Thành viên B
*   **Nhiệm vụ chung**: Tìm hiểu lý thuyết cơ bản về Power BI, phụ trách tiền xử lý dữ liệu thô (Power Query).
*   **Mục tiêu phân tích riêng (Mục tiêu 2) - Phân tích Phân loại Đối tượng & Danh mục (Category/Classification Analysis)**:
    *   *Nội dung*: Phân tích cơ cấu và hiệu suất của các danh mục, phân loại hoặc nhóm đối tượng chính trong bộ dữ liệu (Ví dụ: nhóm sản phẩm, nhóm dịch vụ, thể loại, khu vực...) nhằm xác định đối tượng đóng góp nhiều nhất hoặc kém hiệu quả nhất.
    *   *Biểu đồ phụ trách*: Biểu đồ cột nằm ngang (Bar Chart), biểu đồ hình cây (Treemap), hoặc biểu đồ tròn/vành khuyên (Pie/Donut Chart).
*   **Tiến trình công việc chi tiết**:
    *   **Ngày 1 - 3**: Nghiên cứu lý thuyết Power BI; viết phần giới thiệu công cụ Power BI trong báo cáo.
    *   **Ngày 4 - 5**: Tiếp nhận raw dataset, dùng Power Query để làm sạch dữ liệu (xử lý null, chuẩn hóa kiểu dữ liệu, lọc nhiễu) và bàn giao lại cho Thành viên A.
    *   **Ngày 6 - 9**: Thực hiện phân tích Mục tiêu 2 trên Power BI. Viết phần báo cáo cho mục tiêu này.
    *   **Ngày 10 - 12**: Chụp hình ảnh biểu đồ, viết báo cáo chi tiết phần phân tích mục tiêu 2 (giải thích ý nghĩa biểu đồ và lý do chọn màu sắc).
    *   **Ngày 13 - 14**: Tham gia thuyết trình phần mình phụ trách trong video demo và kiểm tra chéo file Power BI trước khi nộp.

### 👤 Thành viên C
*   **Nhiệm vụ chung**: Nghiên cứu các kỹ thuật tạo tương tác trên Dashboard (Slicers, Filters, Tooltips) và điều hướng.
*   **Mục tiêu phân tích riêng (Mục tiêu 3) - Phân tích Hành vi & Phân khúc Nhóm Chủ thể (Segment/Subject Analysis)**:
    *   *Nội dung*: Phân tích sâu hành vi và thuộc tính của các nhóm chủ thể chính tham gia vào dữ liệu (Ví dụ: khách hàng, người dùng, nhân viên, chi nhánh...). Đo lường các chỉ số trung bình và xếp hạng các chủ thể nổi bật.
    *   *Biểu đồ phụ trách*: Bảng ma trận (Matrix/Table), biểu đồ cột chồng (Stacked Chart) hoặc biểu đồ phân tán (Scatter Plot) phân khúc nhóm chủ thể.
*   **Tiến trình công việc chi tiết**:
    *   **Ngày 1 - 3**: Nghiên cứu các kỹ thuật UX/UI trên Dashboard và thiết kế bộ lọc tương tác.
    *   **Ngày 4 - 5**: Phối hợp với Thành viên A kiểm tra tính chính xác của mô hình dữ liệu bằng các phép tính DAX cơ bản.
    *   **Ngày 6 - 9**: Thực hiện phân tích Mục tiêu 3 trên Power BI. Viết phần báo cáo cho mục tiêu này.
    *   **Ngày 8 - 9**: Phối hợp với Thành viên A chèn các bộ lọc động (Slicers) và Tooltips giúp người xem tương tác sâu với dữ liệu trên Dashboard.
    *   **Ngày 10 - 12**: Chụp ảnh biểu đồ và viết báo cáo phần phân tích mục tiêu 3 (rút ra các insight hành vi).
    *   **Ngày 13 - 14**: Tham gia thuyết trình phần mình phụ trách trong video demo và hỗ trợ đóng gói sản phẩm.

### 👤 Thành viên D
*   **Nhiệm vụ chung**: Biên tập tài liệu báo cáo bằng LaTeX, quay phim và biên tập video thuyết trình giới thiệu đồ án.
*   **Mục tiêu phân tích riêng (Mục tiêu 4) - Phân tích Mối tương quan & Hiệu quả Vận hành (Correlation & Operational Analysis)**:
    *   *Nội dung*: Phân tích mối tương quan giữa các biến số đo lường (Ví dụ: chiết khấu vs lợi nhuận, chi phí vs doanh thu, thời gian xử lý vs chất lượng...) nhằm tìm ra quy luật hoặc các điểm tối ưu vận hành.
    *   *Biểu đồ phụ trách*: Biểu đồ phân tán (Scatter Chart) kết hợp đường xu hướng, biểu đồ thác nước (Waterfall Chart), hoặc biểu đồ kết hợp (Combo Chart).
*   **Tiến trình công việc chi tiết**:
    *   **Ngày 1 - 3**: Khởi tạo sườn báo cáo LaTeX (`main.tex`, `coverpage.tex` và cấu trúc các thư mục) để cả nhóm bắt đầu điền nội dung.
    *   **Ngày 4 - 5**: Chuẩn bị các cấu trúc bảng (Table) thông tin nhóm, thông tin bảng dữ liệu nguồn trong LaTeX.
    *   **Ngày 6 - 9**: Thực hiện phân tích Mục tiêu 4 trên Power BI. Viết phần báo cáo cho mục tiêu này.
    *   **Ngày 10 - 12**: Thu thập nội dung viết của 3 thành viên còn lại, đưa toàn bộ nội dung, bảng biểu, ảnh chụp biểu đồ vào file LaTeX, căn chỉnh lề và biên dịch ra file PDF hoàn chỉnh.
    *   **Ngày 13 - 14**: Dựng video thuyết trình từ các phân đoạn quay của nhóm, chỉnh sửa hiệu ứng và xuất video cuối cùng. Hỗ trợ đóng gói sản phẩm nộp bài.

---

## 3. Checklist Sản phẩm Bàn giao theo Hạn chót

| Ngày | Sản phẩm bàn giao | Người chịu trách nhiệm | Trạng thái |
| :--- | :--- | :--- | :--- |
| **Ngày 3** | Chọn xong chủ đề, bộ dữ liệu & Viết lý thuyết PBI | Cả nhóm | `[ ] Chưa đầu` |
| **Ngày 5** | Dữ liệu được làm sạch & Mô hình hóa (Data Model) | Thành viên B, A | `[ ] Chưa đầu` |
| **Ngày 9** | Biểu đồ của 4 mục tiêu phân tích cá nhân hoàn thành | Cả nhóm | `[ ] Chưa đầu` |
| **Ngày 10** | Dashboard tương tác tổng hợp (đã cấu hình bộ lọc) | Thành viên A, C | `[ ] Chưa đầu` |
| **Ngày 12** | File báo cáo LaTeX được biên dịch thành công ra PDF | Thành viên D | `[ ] Chưa đầu` |
| **Ngày 13** | Video demo dashboard và thuyết trình hoàn thiện | Thành viên D, Cả nhóm | `[ ] Chưa đầu` |
| **Ngày 14** | Đóng gói file zip `[MSSV_1, MSSV_2, MSSV_3].zip` & Nộp bài | Cả nhóm | `[ ] Chưa đầu` |

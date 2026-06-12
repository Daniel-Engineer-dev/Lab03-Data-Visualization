# TIÊU CHÍ PHÊ DUYỆT NGUỒN DỮ LIỆU ĐỒ ÁN
## Lab 03: Trực quan hóa dữ liệu bằng Power BI

Tài liệu này quy định các tiêu chuẩn kỹ thuật và nghiệp vụ để kiểm tra, đánh giá và phê duyệt một bộ dữ liệu (dataset) trước khi nhóm tiến hành triển khai xây dựng data model và dashboard.

---

## 1. Tiêu chí Kỹ thuật (Technical Criteria)

### 1.1. Tính chất dữ liệu quan hệ (Relational Structure) - Bắt buộc
-   Bộ dữ liệu **không được là một bảng phẳng duy nhất (single flat table)**.
-   Phải chứa ít nhất **từ 2 đến 3 bảng riêng biệt** trở lên.
-   Có sự phân chia rõ ràng giữa các bảng chứa dữ liệu đo lường/giao dịch (**Fact Table**) và các bảng danh mục/thông tin đối tượng (**Dimension Tables**).
-   Các trường khóa chính (Primary Key - PK) và khóa ngoại (Foreign Key - FK) phải được định nghĩa rõ ràng để có thể liên kết dạng 1-nhiều ($1:\infty$) hoặc 1-1 ($1:1$). Hạn chế tối đa quan hệ nhiều-nhiều ($\infty:\infty$).

### 1.2. Kích thước và Độ phong phú của Dữ liệu (Data Volume & Richness)
-   **Kích thước**: Bảng dữ liệu chính (Fact table) phải có độ lớn tối thiểu từ **1,000 dòng dữ liệu** trở lên để đảm bảo các biểu đồ có ý nghĩa thống kê và thể hiện rõ xu hướng.
-   **Chiều thời gian**: Phải có ít nhất một trường dữ liệu dạng ngày tháng (Date/DateTime) để phục vụ phân tích thời gian và vẽ biểu đồ xu hướng.
-   **Trường định lượng (Numeric facts)**: Phải chứa tối thiểu 2-3 cột số liệu định lượng có thể tính toán được (ví dụ: doanh số, lợi nhuận, chi phí, điểm số, thời gian xử lý...).
-   **Trường định tính (Categorical dimensions)**: Phải có ít nhất 3-4 trường định tính để lọc và phân nhóm dữ liệu (ví dụ: phân khúc, quốc gia, loại sản phẩm, trạng thái...).

### 1.3. Chất lượng Dữ liệu (Data Quality & Cleanability)
-   **Tỷ lệ dữ liệu khuyết**: Các cột chứa thông tin khóa liên kết hoặc các trường số đo lường chính không được khuyết dữ liệu quá 5%. Các trường thông tin phụ trợ khác không được khuyết quá 15%.
-   **Khả năng làm sạch**: Dữ liệu thô phải có định dạng tương đối đồng nhất để có thể tiền xử lý dễ dàng bằng Power Query (không bị lỗi font hệ thống nghiêm trọng hoặc cấu trúc file bị xáo trộn quá lớn).

---

## 2. Tiêu chí Nghiệp vụ & Khả năng Phân công (Functional & Team Criteria)

### 2.1. Khả năng phân chia 4 mục tiêu phân tích độc lập
Bộ dữ liệu phải cung cấp đầy đủ thông tin để phân chia đều cho 4 thành viên thực hiện phân tích 4 khía cạnh riêng biệt theo sườn tổng quát:
1.  **Khía cạnh 1 (Thời gian & Vĩ mô)**: Dữ liệu phải có tính chu kỳ hoặc phân phối thời gian đủ rộng (ví dụ: trải dài qua nhiều năm hoặc nhiều tháng).
2.  **Khía cạnh 2 (Phân loại danh mục)**: Dữ liệu có các trường phân loại nhiều cấp (ví dụ: Danh mục lớn $\rightarrow$ Danh mục con $\rightarrow$ Chi tiết cụ thể).
3.  **Khía cạnh 3 (Phân khúc nhóm chủ thể)**: Dữ liệu có thông tin về các tác nhân giao dịch (ví dụ: Khách hàng, chi nhánh, nhà cung cấp, nhân viên...) để xếp hạng và phân khúc hành vi.
4.  **Khía cạnh 4 (Tương quan & Hiệu quả)**: Dữ liệu có các biến số có khả năng tác động qua lại lẫn nhau (ví dụ: mức chiết khấu ảnh hưởng đến lợi nhuận, hoặc phương thức vận chuyển ảnh hưởng đến thời gian giao hàng).

### 2.2. Tính thực tiễn và Khả năng khai phá Insights
-   Bộ dữ liệu mô tả một bài toán thực tế (Kinh doanh, Y tế, Giáo dục, Vận tải, Công nghệ, Thể thao...).
-   Dữ liệu không quá đơn giản hoặc hiển nhiên. Phải chứa đựng các mâu thuẫn hoặc xu hướng cần phân tích mới tìm ra nguyên nhân (ví dụ: doanh số cao nhưng lợi nhuận âm, hoặc thời gian xử lý đơn hàng bị trễ ở một số chi nhánh cụ thể).

---

## 3. Tiêu chí Pháp lý & Bản quyền (Legal & Accessibility)

-   **Nguồn gốc rõ ràng**: Dữ liệu từ các cổng dữ liệu mở uy tín hoặc các nghiên cứu có nguồn dẫn rõ ràng.
-   **Bảo mật thông tin**: Bộ dữ liệu không chứa các thông tin nhạy cảm của cá nhân thực tế (PII - Personally Identifiable Information như Số CCCD, số thẻ tín dụng, số điện thoại thật...) trừ khi đã được mã hóa/anonymize.
-   **Tính công khai**: Dữ liệu có thể chia sẻ công khai lên Google Drive hoặc đính kèm trong thư mục nộp bài mà không vi phạm chính sách bảo mật của bên thứ ba.

# TIÊU CHÍ NGHIỆM THU ĐỒ ÁN (LAB 03)
## Hệ thống Dashboard & Báo cáo Phân tích (Nhóm 15)

Tài liệu này quy định các tiêu chuẩn để kiểm tra chất lượng sản phẩm cuối cùng của đồ án, đảm bảo số liệu nhất quán, hình ảnh đồng bộ và báo cáo chính xác trước khi nộp bài.

---

## 1. Tiêu chí Dữ liệu sạch & Mô hình hóa (Clean Data & Model)
*Mục tiêu: Đảm bảo dữ liệu được tiền xử lý đúng quy định và mô hình hóa chuẩn xác.*

- [ ] **Làm sạch hoàn toàn trong Power Query:** Toàn bộ bước làm sạch, xử lý dữ liệu thiếu (`Unknown`, `Unallocated`) và giải mã nhãn phải thực hiện trực tiếp trong Power BI. Không sử dụng công cụ ngoài (Python, R, Excel) để clean trước.
- [ ] **Giải mã tiếng Việt đầy đủ:** Tất cả các trục biểu đồ, legend và slicer phải sử dụng cột tiếng Việt đã giải mã (Ví dụ: `Thành thị/Nông thôn`, `Nam/Nữ`, `Tử vong/Nghiêm trọng/Nhẹ`).
- [ ] **Quan hệ dữ liệu chuẩn xác:** Quan hệ giữa các bảng phải là quan hệ 1-nhiều ($1:\infty$) đi từ các bảng Dimension (`Calendar`, `Casualties`, `Vehicles`) đến bảng Fact (`Collisions`) hoặc thông qua các trường khóa ngoại hợp lệ.
- [ ] **Tránh tự động cộng dồn (Auto-sum):** Các trường số không dùng để tính toán (như `Year`, `speed_limit`) phải được chuyển về dạng **Text** hoặc định dạng qua DAX (như tạo cột `Tốc độ VN` chứa chữ `"mph"`) để tránh bị Power BI tự động cộng tổng (`Sum`) thành `2K`, `200K` trên các thẻ KPI.
- [ ] **Sắp xếp đúng thứ tự (Sorting):** 
  - Trục thời gian (Tháng) phải được sắp xếp theo `Month Number` (từ tháng 1 đến tháng 12).
  - Thứ trong tuần phải được sắp xếp từ Thứ 2 đến Chủ nhật.
  - Nhóm tuổi phải sắp xếp theo thứ tự tự nhiên (từ nhỏ đến lớn: `0-5`, `6-10`,..., `Over 75`).

---

## 2. Tiêu chí Khớp số liệu giữa Phân tích & Hình ảnh (Data & Insight Matching)
*Mục tiêu: Đảm bảo các con số, biểu đồ và nhận xét trong báo cáo khớp hoàn toàn với thực tế dữ liệu.*

- [ ] **Khớp số liệu KPI Tổng quan (Trang 1 vs Toàn bộ):** Khi các Slicer ở trạng thái mặc định (`All`), các con số tổng phải khớp nhau trên mọi trang:
  - Tổng số vụ va chạm: **503K** (Chính xác: 503.475)
  - Tổng số người thương vong: **641K** (Chính xác: 640.522)
  - Tổng số phương tiện liên quan: **921K** (Chính xác: 920.692)
  - Số người tử vong: **8K** (Chính xác: 7.955)
- [ ] **Khớp số liệu xu hướng thời gian (Trang 2):**
  - Năm cao điểm tai nạn: **2022**
  - Tháng xảy ra nhiều tai nạn nhất: **Tháng 10**
  - Thứ xảy ra nhiều tai nạn nhất: **Thứ 6**
  - Giờ cao điểm xảy ra nhiều tai nạn nhất: **17:00**
- [ ] **Khớp số liệu điều kiện đường sá (Trang 3):**
  - Loại đường xảy ra nhiều tai nạn nhất: **Đường đơn** (Single carriageway)
  - Điều kiện thời tiết xảy ra nhiều tai nạn nhất: **Nắng (không gió)** (Fine no high winds)
  - Giới hạn tốc độ xảy ra nhiều tai nạn nhất: **30 mph**
  - Tình trạng mặt đường xảy ra nhiều tai nạn nhất: **Khô ráo** (Dry)
- [ ] **Khớp số liệu phương tiện & người lái (Trang 4):**
  - Loại xe xảy ra nhiều tai nạn nhất: **Ô tô** (Car)
  - Giới tính tài xế phổ biến nhất: **Nam** (Male)
  - Nhóm tuổi tài xế phổ biến nhất: **26 - 35**
  - Khu vực xảy ra nhiều tai nạn phương tiện nhất: **Thành thị** (Urban, chiếm 67%)
- [ ] **Khớp số liệu người thương vong (Trang 5):**
  - Giới tính thương vong phổ biến nhất: **Nam**
  - Nhóm tuổi thương vong phổ biến nhất: **26 - 35**
  - Vai trò thương vong phổ biến nhất: **Người điều khiển** (Driver or rider)
- [ ] **Sửa lỗi lọc thẻ KPI (Apply Filter):** Đảm bảo tất cả các thẻ KPI lọc theo Top 1 (như *Giờ cao điểm*, *Vai trò phổ biến*, *Loại xe phổ biến*) đã được bấm nút **`Apply filter`** trong ngăn Filters. Thẻ không được hiển thị giá trị đầu tiên theo alphabet do quên lưu bộ lọc (Ví dụ: Thẻ vai trò phải hiển thị đúng là `"Người điều khiển"`, không phải `"Hành khách"`).

---

## 3. Tiêu chí Hình ảnh Đồng bộ (Image & Layout Matching)
*Mục tiêu: Đảm bảo ảnh chụp màn hình trong báo cáo phản ánh đúng giao diện hiện tại của Dashboard.*

- [ ] **Đồng bộ ảnh chụp thực tế:** Toàn bộ ảnh trực quan hóa trong báo cáo LaTeX (nằm trong thư mục `report/images/`) phải được chụp trực tiếp từ Dashboard Power BI sau khi đã hoàn thiện làm sạch, đổi màu sắc và dịch tiếng Việt.
- [ ] **Không sử dụng ảnh giữ chỗ (Placeholder):** Đảm bảo không còn các hình hộp xám, văn bản mẫu (`Vị trí chèn ảnh...`) hay dữ liệu mẫu doanh số (Sales sample) trong báo cáo.
- [ ] **Không lỗi hiển thị giao diện:**
  - Không có thẻ KPI nào bị khuất chữ (ví dụ: bị hiển thị dạng `Người điểu k...` hay `Nắng (khôn...` do kích thước chữ quá lớn). Cỡ chữ của Callout value trên các thẻ KPI dài nên chỉnh về **20pt** để hiển thị trọn vẹn.
  - Các nhãn biểu đồ Deneb không bị đè lên nhau, trục tọa độ không bị mất nhãn hoặc tràn viền.
- [ ] **Trạng thái bộ lọc khi chụp ảnh:** Khi chụp ảnh giao diện trang tổng quan hoặc các trang thành phần để chèn vào báo cáo, các Slicer phải được **nhả lọc về trạng thái mặc định (All)** để số liệu hiển thị trên ảnh là số liệu tổng quát, tránh gây mâu thuẫn số liệu giữa các trang báo cáo.

---

## 4. Tiêu chí Yêu cầu Đề bài (Assignment Requirements)
*Mục tiêu: Đảm bảo tuân thủ đầy đủ các quy định về mặt học thuật và kỹ thuật của đồ án.*

- [ ] **Đầy đủ 16 biểu đồ chính:** Hệ thống báo cáo/dashboard phải có đủ 16 biểu đồ chính được phân bổ đều cho 4 mục tiêu phân tích của 4 thành viên.
- [ ] **Đầy đủ các nhận xét phân tích (Insights):** Mỗi mục tiêu phân tích cá nhân trong Chương 4 phải có từ **3 đến 4 nhận xét liên kết** có dẫn chứng số liệu trực tiếp từ biểu đồ.
- [ ] **Giới hạn số trang báo cáo:** Báo cáo PDF cuối cùng sau khi biên dịch không được vượt quá **24 trang**.
- [ ] **Mô hình hóa dữ liệu (Mục 2):** Báo cáo phải có sơ đồ hình ảnh Data Model thực tế và phần giải thích rõ ràng về cấu trúc bảng (Fact, Dimension), các trường khóa liên kết.
- [ ] **Nhận xét kết luận và khuyến nghị (Chương 5):** Chương 5 phải hoàn thiện đầy đủ phần tổng hợp insights liên kết chéo giữa các mục tiêu, đề xuất khuyến nghị cụ thể dựa trên số liệu thực tế, chỉ ra hạn chế của đồ án và danh mục tài liệu tham khảo đầy đủ.
- [ ] **Biên dịch LaTeX thành công:** File `report/main.pdf` phải được build thành công, không có lỗi cú pháp nghiêm trọng, không còn các cảnh báo liên kết bị thiếu (`??` hoặc `undefined references`).

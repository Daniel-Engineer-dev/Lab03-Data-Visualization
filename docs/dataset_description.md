# TÀI LIỆU MÔ TẢ DATASET VÀ HƯỚNG DẪN TRỰC QUAN HÓA (LAB 03)

Tài liệu này cung cấp đầy đủ thông tin kỹ thuật về cấu trúc dữ liệu, các mối quan hệ, danh sách các Measure DAX và hướng dẫn ánh xạ trực quan hóa cho từng mục tiêu phân tích cá nhân trong đồ án thực hành Lab 03. Tài liệu được thiết kế để các Agent và thành viên nhóm 15 có thể dựa vào để viết code hoặc thiết lập biểu đồ một cách nhất quán và chính xác.

---

## 1. Tổng quan cấu trúc Mô hình dữ liệu (Data Model Overview)

Mô hình dữ liệu được thiết kế theo dạng **Extended Star Schema (Sơ đồ hình sao mở rộng)** với bảng trung tâm là `Collisions`.

### Sơ đồ quan hệ và liên kết:
*   **Bảng trung tâm (Fact chính):** `Collisions`
*   **Bảng chi tiết (Fact chi tiết):**
    *   `Casualties` (Chứa thông tin người bị thương/tử vong). Quan hệ $1:\ast$ với `Collisions` qua trường `collision_index`.
    *   `Vehicles` (Chứa thông tin phương tiện liên quan). Quan hệ $1:\ast$ với `Collisions` qua trường `collision_index`.
*   **Bảng thời gian:** `Calendar` (Tự tạo trong Power Query/DAX) liên kết với cột `date` của bảng `Collisions`.

---

## 2. Chi tiết các bảng và trường dữ liệu (Schema Details)

Mỗi bảng chứa hai loại cột:
*   **Cột code gốc (ID/Code):** Giá trị dạng số hoặc mã gốc, dùng cho tính toán, viết measure hoặc đối chiếu logic.
*   **Cột label đã giải mã (`_label`):** Đã ánh xạ sang tiếng Anh dễ đọc, dùng để hiển thị trên Trục (Axis), Legend, Slicer, Tooltip hoặc Bảng/Matrix.

### 2.1. Bảng `Collisions` (Dữ liệu về vụ va chạm - Fact chính)
Một dòng tương ứng với một vụ tai nạn giao thông độc lập.

| Tên Cột thực tế | Kiểu dữ liệu | Loại cột | Mô tả và Ý nghĩa |
|---|---|---|---|
| `collision_index` | String | Khóa chính | ID duy nhất của vụ va chạm |
| `collision_year` | Int64 | Code gốc | Năm xảy ra tai nạn (2020 - 2024) |
| `date` | DateTime | Khóa ngoại | Ngày xảy ra tai nạn (Liên kết với Calendar) |
| `time` | DateTime | Code gốc | Giờ xảy ra tai nạn |
| `longitude` | Double | Bản đồ | Kinh độ xảy ra tai nạn |
| `latitude` | Double | Bản đồ | Vĩ độ xảy ra tai nạn |
| `number_of_vehicles` | Int64 | Code gốc | Số lượng phương tiện tham gia trong vụ va chạm |
| `number_of_casualties` | Int64 | Code gốc | Số lượng người thương vong trong vụ va chạm |
| `speed_limit` | Int64 | Code gốc | Giới hạn tốc độ của đoạn đường (20, 30, 40, 50, 60, 70 mph) |
| `collision_severity_label` | String | **Label** | Mức độ nghiêm trọng vụ va chạm (`Fatal`, `Serious`, `Slight`) |
| `road_type_label` | String | **Label** | Loại đường (`Single carriageway`, `Dual carriageway`, `Roundabout`,...) |
| `light_conditions_label` | String | **Label** | Điều kiện ánh sáng (`Daylight`, `Darkness - lights lit`, `Darkness - no lighting`,...) |
| `weather_conditions_label`| String | **Label** | Điều kiện thời tiết (`Fine no high winds`, `Raining no high winds`, `Snowing`,...) |
| `road_surface_conditions_label`| String| **Label** | Tình trạng mặt đường (`Dry`, `Wet or damp`, `Snow`, `Frost or ice`,...) |
| `junction_detail_label` | String | **Label** | Chi tiết nút giao (`Not at junction`, `T or staggered junction`, `Roundabout`,...) |
| `junction_control_label` | String | **Label** | Điều khiển nút giao (`Give way or uncontrolled`, `Auto traffic signal`,...) |
| `urban_or_rural_area_label`| String | **Label** | Phân loại khu vực (`Urban`, `Rural`, `Unallocated`) |
| `day_of_week_label` | String | **Label** | Ngày trong tuần (`Monday`, `Tuesday`, `Wednesday`,...) |

### 2.2. Bảng `Vehicles` (Dữ liệu về phương tiện - Fact chi tiết)
Một dòng tương ứng với một phương tiện trong một vụ va chạm. Một vụ va chạm (`collision_index`) có thể có nhiều phương tiện.

| Tên Cột thực tế | Kiểu dữ liệu | Loại cột | Mô tả và Ý nghĩa |
|---|---|---|---|
| `collision_index` | String | Khóa ngoại | Liên kết về bảng `Collisions` |
| `vehicle_reference` | Int64 | Code gốc | Thứ tự phương tiện trong vụ va chạm (1, 2, 3...) |
| `age_of_driver` | Int64 | Code gốc | Tuổi thực tế của người lái xe (Giá trị âm `-1` là dữ liệu thiếu) |
| `sex_of_driver_label` | String | **Label** | Giới tính người lái (`Male`, `Female`, `Unknown/Not provided`) |
| `age_band_of_driver_label`| String | **Label** | Nhóm tuổi người lái (`16-20`, `21-25`, `26-35`, `36-45`, `Over 75`,...) |
| `vehicle_type_label` | String | **Label** | Loại phương tiện (`Car`, `Motorcycle`, `Bus or coach`, `Van / Goods`,...) |

### 2.3. Bảng `Casualties` (Dữ liệu về người thương vong - Fact chi tiết)
Một dòng tương ứng với một người bị thương hoặc tử vong. Một vụ va chạm (`collision_index`) có thể có nhiều người thương vong.

| Tên Cột thực tế | Kiểu dữ liệu | Loại cột | Mô tả và Ý nghĩa |
|---|---|---|---|
| `collision_index` | String | Khóa ngoại | Liên kết về bảng `Collisions` |
| `vehicle_reference` | Int64 | Khóa ngoại | Liên kết đến phương tiện mà nạn nhân ngồi trên (nếu có) |
| `age_of_casualty` | Int64 | Code gốc | Tuổi của nạn nhân (Giá trị âm `-1` là dữ liệu thiếu) |
| `casualty_severity_label` | String | **Label** | Mức độ thương vong (`Fatal`, `Serious`, `Slight`) |
| `casualty_class_label` | String | **Label** | Vai trò của nạn nhân (`Driver or rider`, `Passenger`, `Pedestrian`) |
| `sex_of_casualty_label` | String | **Label** | Giới tính nạn nhân (`Male`, `Female`, `Unknown/Not provided`) |
| `age_band_of_casualty_label`| String| **Label** | Nhóm tuổi nạn nhân (`0-5`, `6-10`, `16-20`, `26-35`, `Over 75`,...) |

---

## 3. Danh sách Measure DAX dùng chung trong Model

Cần dùng chính xác các Measure DAX sau để tính toán các chỉ số vĩ mô thay vì tự kéo cột đếm dòng (nhằm tránh sai lệch grain/bội số đếm):

```dax
-- 1. Tổng số vụ tai nạn
[Total Collisions] = DISTINCTCOUNT ( Collisions[collision_index] )

-- 2. Tổng số phương tiện liên quan
[Total Vehicles] = COUNTROWS ( Vehicles )

-- 3. Tổng số người thương vong
[Total Casualties] = COUNTROWS ( Casualties )

-- 4. Số người tử vong
[Fatal Casualties] = CALCULATE ( [Total Casualties], Casualties[casualty_severity] = 1 )

-- 5. Số người bị thương nặng
[Serious Casualties] = CALCULATE ( [Total Casualties], Casualties[casualty_severity] = 2 )

-- 6. Số người bị thương nhẹ
[Slight Casualties] = CALCULATE ( [Total Casualties], Casualties[casualty_severity] = 3 )

-- 7. Số thương vong trung bình trên một vụ tai nạn
[Average Casualties per Collision] = DIVIDE ( [Total Casualties], [Total Collisions] )
```

---

## 4. Hướng dẫn thiết lập 4 biểu đồ cho từng thành viên

Dưới đây là bảng đặc tả cấu trúc thiết lập trực quan hóa cho từng mục tiêu phân tích cá nhân:

### 4.1. Lê Lâm Trí Đức - Tổng quan và xu hướng thời gian
*   **Mục tiêu chính:** Tìm quy luật biến thiên của tai nạn giao thông theo chu kỳ thời gian (năm, tháng, thứ, giờ) và khu vực.
*   **Bảng dữ liệu sử dụng chính:** `Collisions` kết hợp với bảng `Calendar` (hoặc các trường ngày tháng trong `Collisions`).

| STT | Loại Biểu đồ | Trục X / Y (Axis) | Nhóm (Legend) | Measure (Values) | Bộ lọc visual (Filter) |
|---|---|---|---|---|---|
| **1** | Line Chart | Trục X: `Calendar[Year]` | Legend: `Collisions[collision_severity_label]` | `[Total Collisions]` | Không |
| **2** | Column Chart | Trục X: `Calendar[Month Name]` | Không | `[Total Collisions]` | Sắp xếp tháng theo `Calendar[Month Number]` |
| **3** | Heatmap Matrix | Rows: `Collisions[day_of_week_label]` <br> Columns: `Collisions[time]` (Hour) | Không | `[Total Collisions]` | Sắp xếp ngày theo `day_of_week` |
| **4** | Stacked Bar Chart | Trục Y: `Calendar[Year]` | Legend: `Collisions[urban_or_rural_area_label]` | `[Total Collisions]` | Loại bỏ `Unallocated` |

### 4.2. Hoàng Quốc Việt - Điều kiện đường sá và môi trường
*   **Mục tiêu chính:** Phân tích ảnh hưởng của cơ sở hạ tầng (loại đường, giới hạn tốc độ) và các yếu tố thời tiết, ánh sáng đến tai nạn.
*   **Bảng dữ liệu sử dụng chính:** `Collisions`.

| STT | Loại Biểu đồ | Trục X / Y (Axis) | Nhóm (Legend) | Measure (Values) | Bộ lọc visual (Filter) |
|---|---|---|---|---|---|
| **1** | Stacked Bar Chart | Trục Y: `Collisions[road_type_label]` | Legend: `Collisions[collision_severity_label]` | `[Total Collisions]` | Không |
| **2** | Heatmap Matrix | Rows: `Collisions[weather_conditions_label]` <br> Columns: `Collisions[light_conditions_label]` | Không | `[Total Collisions]` (Hoặc tỷ lệ tai nạn nặng) | Lọc bỏ các nhãn `Unknown` hoặc `Data missing` |
| **3** | Bar Chart | Trục Y: `Collisions[speed_limit]` | Không | `[Total Collisions]` | Sắp xếp trục Y theo thứ tự giảm dần |
| **4** | Clustered Column | Trục X: `Collisions[road_surface_conditions_label]`| Legend: `Collisions[urban_or_rural_area_label]` | `[Total Collisions]` | Lọc bỏ `Unallocated` và `Unknown` |

### 4.3. Nguyễn Lê Thế Vinh - Phương tiện và người lái
*   **Mục tiêu chính:** Phân tích chân dung người điều khiển (tuổi, giới tính) và các phương tiện chịu ảnh hưởng lớn nhất.
*   **Bảng dữ liệu sử dụng chính:** `Vehicles`.

| STT | Loại Biểu đồ | Trục X / Y (Axis) | Nhóm (Legend) | Measure (Values) | Bộ lọc visual (Filter) |
|---|---|---|---|---|---|
| **1** | Bar Chart | Trục Y: `Vehicles[vehicle_type_label]` | Không | `[Total Vehicles]` | Top 10 hoặc lọc bỏ các loại xe quá ít |
| **2** | Stacked Column | Trục X: `Vehicles[age_band_of_driver_label]` | Legend: `Vehicles[sex_of_driver_label]` | `[Total Vehicles]` | Loại bỏ `Data missing/out of range` hoặc `Unknown` |
| **3** | Treemap / Donut | Category: `Collisions[urban_or_rural_area_label]` | Không | `[Total Vehicles]` | Loại bỏ `Unallocated` |
| **4** | Line/Column Chart | Trục X: `Vehicles[age_band_of_driver_label]` | Không | Cột: `[Total Vehicles]` <br> Đường: Tỷ lệ tai nạn nặng | Loại bỏ `Data missing/out of range` |

### 4.4. Phạm Quang Vinh - Người thương vong và nhóm rủi ro
*   **Mục tiêu chính:** Nhận diện những người bị tổn thương trực tiếp (tuổi, giới tính, vai trò tham gia giao thông) để đưa ra khuyến nghị an toàn.
*   **Bảng dữ liệu sử dụng chính:** `Casualties`.

| STT | Loại Biểu đồ | Trục X / Y (Axis) | Nhóm (Legend) | Measure (Values) | Bộ lọc visual (Filter) |
|---|---|---|---|---|---|
| **1** | Stacked Bar Chart | Trục Y: `Casualties[age_band_of_casualty_label]` | Legend: `Casualties[casualty_severity_label]` | `[Total Casualties]` | Loại bỏ `Data missing/out of range` |
| **2** | Bar Chart | Trục Y: `Casualties[casualty_class_label]` | Không | `[Total Casualties]` | Không |
| **3** | Clustered Column | Trục X: `Casualties[age_band_of_casualty_label]` | Legend: `Casualties[sex_of_casualty_label]` | `[Total Casualties]` | Lọc bỏ `Data missing/out of range` và `Unknown` |
| **4** | 100% Stacked Column| Trục X: `Casualties[casualty_class_label]` | Legend: `Casualties[casualty_severity_label]` | `[Total Casualties]` | Sắp xếp để làm nổi bật tỷ lệ Fatal/Serious |

---

## 5. Nguyên tắc chung khi viết code phân tích & nhận xét (Guidelines for Agents)

1.  **Nhất quán về Số liệu:** Luôn đối chiếu tổng số của các visual riêng lẻ với tổng số trên các thẻ KPI chung (`Total Collisions`, `Total Vehicles`, `Total Casualties`) để đảm bảo không bị nhân đôi số liệu do join sai quan hệ.
2.  **Lọc dữ liệu thiếu:** Đối với các thuộc tính định tính (ví dụ: nhóm tuổi, giới tính), khi đưa lên visual biểu đồ cần áp dụng bộ lọc visual loại bỏ các nhãn `Data missing/out of range`, `Unknown` để tránh biểu đồ bị loãng, tập trung phân tích vào các nhóm hợp lệ.
3.  **Tương tác chéo (Cross-filtering):** Đảm bảo các slicer về Năm (`Calendar[Year]`), Giới tính và Mức độ nghiêm trọng hoạt động mượt mà trên tất cả các biểu đồ để hỗ trợ phân tích drill-down.

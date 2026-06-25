# Hướng dẫn sử dụng các cột label và measure trong Power BI

Tài liệu này dành cho các thành viên nhóm 15 sau khi file Power BI nền đã được tiền xử lý. Mục tiêu là giúp mọi người biết nên dùng cột nào khi vẽ biểu đồ, dùng measure nào để đếm đúng, và xử lý các giá trị `Unknown`, `Not applicable`, `Data missing/out of range` như thế nào.

## 1. Nguyên tắc chung

Trong model có hai loại cột:

| Loại cột | Ví dụ | Cách dùng |
|---|---|---|
| Cột code gốc | `casualty_severity`, `vehicle_type`, `road_type` | Dùng để kiểm tra, đối chiếu Data Guide, hoặc viết measure cần code ổn định |
| Cột label đã giải mã | `casualty_severity_label`, `vehicle_type_label`, `road_type_label` | Dùng cho trục biểu đồ, legend, slicer và bảng/matrix |

Khi vẽ biểu đồ, ưu tiên dùng cột có hậu tố:

```text
_label
```

Không nên đưa trực tiếp các cột code như `1`, `2`, `3`, `9`, `-1` lên trục biểu đồ vì người đọc không hiểu ý nghĩa.

## 2. Các measure dùng chung

Dùng các measure này thay vì tự kéo cột rồi để Power BI tự đếm.

| Measure | Ý nghĩa | Khi dùng |
|---|---|---|
| `Total Collisions` | Tổng số vụ va chạm | KPI, xu hướng thời gian, điều kiện đường/môi trường |
| `Total Vehicles` | Tổng số phương tiện liên quan | Phân tích phương tiện |
| `Total Casualties` | Tổng số người thương vong | Phân tích thương vong |
| `Fatal Casualties` | Số người tử vong | Khi cần tách mức độ nghiêm trọng |
| `Serious Casualties` | Số người bị thương nặng | Khi cần tách mức độ nghiêm trọng |
| `Slight Casualties` | Số người bị thương nhẹ | Khi cần tách mức độ nghiêm trọng |
| `Average Casualties per Collision` | Trung bình thương vong trên mỗi vụ | KPI hoặc nhận xét tổng quan |

Không nên đếm collision bằng `COUNTROWS(Vehicles)` hoặc `COUNTROWS(Casualties)`, vì mỗi vụ có thể có nhiều phương tiện và nhiều thương vong.

## 3. Bảng Collisions

Bảng `Collisions` có đơn vị dòng là:

```text
1 dòng = 1 vụ va chạm
```

Dùng bảng này cho các phân tích về thời gian, điều kiện đường, ánh sáng, thời tiết, mặt đường và mức độ vụ va chạm.

### Cột label nên dùng

| Cột label | Ý nghĩa | Dùng cho |
|---|---|---|
| `collision_severity_label` | Mức độ nghiêm trọng của vụ va chạm | Legend, slicer, stacked bar |
| `day_of_week_label` | Ngày trong tuần | Trục biểu đồ, heatmap |
| `road_type_label` | Loại đường | Bar chart, slicer |
| `light_conditions_label` | Điều kiện ánh sáng | Matrix, slicer |
| `weather_conditions_label` | Điều kiện thời tiết | Matrix, slicer |
| `road_surface_conditions_label` | Tình trạng mặt đường | Bar chart, slicer |
| `junction_detail_label` | Chi tiết nút giao | Phân tích nâng cao |
| `junction_control_label` | Điều khiển nút giao | Phân tích nâng cao |
| `urban_or_rural_area_label` | Khu vực đô thị/nông thôn | Slicer, so sánh nhóm |

### Ví dụ dùng đúng

Biểu đồ số vụ theo loại đường:

```text
Trục Y: Collisions[road_type_label]
Giá trị: [Total Collisions]
```

Matrix thời tiết và ánh sáng:

```text
Rows: Collisions[weather_conditions_label]
Columns: Collisions[light_conditions_label]
Values: [Total Collisions]
```

## 4. Bảng Vehicles

Bảng `Vehicles` có đơn vị dòng là:

```text
1 dòng = 1 phương tiện trong 1 vụ va chạm
```

Dùng bảng này cho phân tích loại phương tiện và đặc điểm người lái.

### Cột label nên dùng

| Cột label | Ý nghĩa | Dùng cho |
|---|---|---|
| `vehicle_type_label` | Loại phương tiện | Bar chart, slicer |
| `sex_of_driver_label` | Giới tính người lái | Slicer, stacked chart |
| `age_band_of_driver_label` | Nhóm tuổi người lái | Trục biểu đồ, stacked column |

### Cột cleaned nên dùng

| Cột | Ý nghĩa | Khi dùng |
|---|---|---|
| `age_of_driver_clean` | Tuổi người lái, giá trị âm đã đổi thành null | Tính trung bình/median tuổi người lái |

Không dùng `age_of_driver` gốc để tính trung bình nếu trong cột còn `-1`, vì `-1` là dữ liệu thiếu/out of range, không phải tuổi thật.

### Ví dụ dùng đúng

Biểu đồ phương tiện:

```text
Trục Y: Vehicles[vehicle_type_label]
Giá trị: [Total Vehicles]
```

Nhóm tuổi người lái:

```text
Trục X: Vehicles[age_band_of_driver_label]
Giá trị: [Total Vehicles]
Legend: Vehicles[sex_of_driver_label]
```

## 5. Bảng Casualties

Bảng `Casualties` có đơn vị dòng là:

```text
1 dòng = 1 người thương vong
```

Dùng bảng này cho phần của Phạm Quang Vinh: người thương vong và nhóm rủi ro.

### Cột label nên dùng

| Cột label | Ý nghĩa | Dùng cho |
|---|---|---|
| `casualty_severity_label` | Mức độ thương vong | Legend, slicer |
| `casualty_class_label` | Vai trò người thương vong | Bar chart, slicer |
| `age_band_of_casualty_label` | Nhóm tuổi người thương vong | Trục biểu đồ |
| `sex_of_casualty_label` | Giới tính người thương vong | Slicer, stacked chart |

### Cột cleaned nên dùng

| Cột | Ý nghĩa | Khi dùng |
|---|---|---|
| `age_of_casualty_clean` | Tuổi người thương vong, giá trị âm đã đổi thành null | Tính trung bình/median tuổi thương vong |

Không dùng `age_of_casualty` gốc để tính trung bình nếu trong cột còn `-1`.

### Ví dụ dùng đúng cho phần của Vinh

Biểu đồ 1: thương vong theo nhóm tuổi và mức độ:

```text
Loại biểu đồ: Stacked bar chart
Trục Y: Casualties[age_band_of_casualty_label]
Giá trị: [Total Casualties]
Legend: Casualties[casualty_severity_label]
```

Biểu đồ 2: thương vong theo vai trò tham gia giao thông:

```text
Loại biểu đồ: Bar chart
Trục Y: Casualties[casualty_class_label]
Giá trị: [Total Casualties]
```

Slicer gợi ý:

```text
Calendar[Year]
Casualties[sex_of_casualty_label]
Casualties[casualty_severity_label]
```

## 6. Bảng Calendar

Bảng `Calendar` dùng để phân tích thời gian và lọc theo năm/tháng/ngày.

| Cột | Dùng cho |
|---|---|
| `Date` | Quan hệ với `Collisions[date]` |
| `Year` | Slicer năm, xu hướng theo năm |
| `Quarter` | Phân tích theo quý |
| `Month Number` | Sắp xếp tháng |
| `Month Name` | Trục tháng |
| `Year Month` | Xu hướng theo tháng-năm |
| `Day of Week Number` | Sắp xếp ngày trong tuần |
| `Day of Week` | Heatmap/ngày trong tuần |

Khi dùng `Month Name`, phải sort theo `Month Number`. Khi dùng `Day of Week`, phải sort theo `Day of Week Number`.

## 7. Cách xử lý Unknown và dữ liệu thiếu khi vẽ biểu đồ

Các nhãn thường gặp:

```text
Unknown
Not applicable
Data missing/out of range
Other
```

Không xóa các dòng này khỏi model chung. Khi vẽ biểu đồ, xử lý theo câu hỏi phân tích:

| Tình huống | Cách xử lý |
|---|---|
| Biểu đồ cần tổng số đầy đủ | Giữ `Unknown`/`Data missing` |
| Biểu đồ cần so sánh nhóm thật, ví dụ nhóm tuổi | Có thể lọc `Data missing/out of range` khỏi riêng visual |
| Báo cáo cần minh bạch chất lượng dữ liệu | Giữ hoặc ghi chú số lượng `Unknown` |

Ví dụ với biểu đồ nhóm tuổi của Vinh, có thể lọc:

```text
age_band_of_casualty_label != Data missing/out of range
```

Không lọc khỏi bảng gốc, chỉ lọc trong visual hoặc page nếu cần.

## 8. Không nên dùng trực tiếp bảng 2024_code_list

Bảng `2024_code_list` là bảng Data Guide dùng để tra mã. Nếu bảng này vẫn xuất hiện trong model, không nên kéo trường của nó vào report chính, trừ khi đang kiểm tra mapping.

Khi vẽ biểu đồ, dùng các cột `_label` đã merge vào `Collisions`, `Vehicles`, `Casualties` thay vì dùng trực tiếp bảng `2024_code_list`.

## 9. Checklist cho từng thành viên

Trước khi vẽ biểu đồ cá nhân:

- [ ] Xác định đúng bảng phân tích: `Collisions`, `Vehicles`, hoặc `Casualties`.
- [ ] Dùng measure chung thay vì tự đếm dòng sai grain.
- [ ] Dùng cột `_label` cho trục, legend, slicer.
- [ ] Kiểm tra `Unknown`/`Data missing` có cần lọc khỏi visual hay không.
- [ ] Ghi lại filter đã dùng để viết nhận xét báo cáo.
- [ ] Không tự sửa relationship hoặc measure chung nếu chưa thống nhất với nhóm.

## 10. Mapping nhanh theo phân công

| Thành viên/phần | Bảng chính | Measure chính | Cột label chính |
|---|---|---|---|
| Tổng quan/xu hướng thời gian | `Collisions`, `Calendar` | `Total Collisions` | `day_of_week_label`, `collision_severity_label` |
| Điều kiện đường sá/môi trường | `Collisions` | `Total Collisions` | `road_type_label`, `weather_conditions_label`, `light_conditions_label`, `road_surface_conditions_label` |
| Phương tiện/người lái | `Vehicles` | `Total Vehicles` | `vehicle_type_label`, `age_band_of_driver_label`, `sex_of_driver_label` |
| Người thương vong/nhóm rủi ro | `Casualties` | `Total Casualties` | `age_band_of_casualty_label`, `casualty_severity_label`, `casualty_class_label`, `sex_of_casualty_label` |

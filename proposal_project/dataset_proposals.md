# Đề xuất dataset và lựa chọn đề tài phân tích

## 1. Mục đích tài liệu

Tài liệu này tổng hợp các dataset đã được cân nhắc cho đồ án Lab 03 - Trực quan hóa dữ liệu bằng Power BI, sau đó chốt dataset được lựa chọn để triển khai phân tích.

Dataset được chọn cuối cùng là:

> **UK Road Safety / STATS19 Road Safety Open Data**

Tên đề tài phân tích đề xuất:

> **Phân tích các yếu tố ảnh hưởng đến mức độ nghiêm trọng của tai nạn giao thông đường bộ tại Vương quốc Anh**

## 2. Tiêu chí lựa chọn dataset

Dataset cần đáp ứng các tiêu chí chính:

- Có cấu trúc quan hệ, không phải một bảng phẳng duy nhất.
- Có ít nhất 2-3 bảng dữ liệu liên kết được qua khóa.
- Fact table chính có trên 1,000 dòng.
- Có trường ngày/thời gian để phân tích xu hướng.
- Có nhiều biến định lượng và định tính.
- Có nguồn công khai, rõ ràng, có thể trích dẫn trong báo cáo.
- Không chứa thông tin cá nhân nhạy cảm.
- Có thể chia thành 4 mục tiêu phân tích độc lập cho các thành viên trong nhóm.
- Phù hợp với báo cáo giới hạn 24 trang.

## 3. Các dataset đã đề xuất

| STT | Dataset | Lĩnh vực | Mức phù hợp | Nhận xét |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Olist Brazilian E-Commerce Public Dataset | Thương mại điện tử | Rất cao | Dataset mạnh, nhiều bảng, nhiều insight; không chọn vì có nhóm khác đã đề xuất. |
| 2 | UK Road Safety / STATS19 | Giao thông, an toàn đường bộ | Rất cao | Được chọn. Nguồn chính phủ, quan hệ rõ giữa collision - vehicle - casualty. |
| 3 | BTS Airline On-Time Performance | Hàng không | Cao | Dữ liệu chính thức, rất giàu KPI vận hành; cần chọn phạm vi vì dữ liệu lớn. |
| 4 | NYC TLC Taxi Trip Record Data | Vận tải đô thị | Cao | Trực quan tốt, có bản đồ; cần xử lý dung lượng và outlier nhiều. |
| 5 | Maven Pizza Place Sales | Bán lẻ/F&B | Trung bình-cao | Dễ làm, nhiều bảng, nhưng dữ liệu mô phỏng nên insight kém thuyết phục hơn. |
| 6 | Global Superstore | Bán lẻ | Trung bình | Dễ làm nhưng dễ bị xem là sample/BI practice dataset và thường phải tự quan hệ hóa. |
| 7 | Instacart Market Basket Analysis | Bán lẻ thực phẩm | Trung bình-cao | Nhiều bảng và dữ liệu lớn, nhưng thiên về market basket/machine learning hơn dashboard nghiệp vụ. |

## 4. Dataset được lựa chọn: UK Road Safety / STATS19

### 4.1. Thông tin chung

- **Tên dataset:** UK Road Safety / STATS19 Road Safety Open Data
- **Cơ quan công bố:** UK Department for Transport
- **Nguồn chính:** https://www.gov.uk/government/statistical-data-sets/road-safety-open-data
- **Catalog tham khảo:** https://www.data.gov.uk/dataset/cb7ae6f0-4be6-4935-9277-47e5ce24a11f/road-accidents-safety-data
- **Lĩnh vực:** Giao thông, an toàn đường bộ, tai nạn và thương vong.
- **Định dạng:** CSV.
- **Giấy phép:** Open Government Licence v3.0.
- **Phạm vi dữ liệu:** Các vụ va chạm gây thương tích cá nhân trên đường công cộng tại Great Britain được báo cáo cho cảnh sát và ghi nhận qua hệ thống STATS19.

### 4.2. Lý do chọn

UK Road Safety / STATS19 là lựa chọn phù hợp nhất vì:

- Không trùng với đề tài Brazilian E-Commerce/Olist của nhóm khác.
- Nguồn dữ liệu chính phủ uy tín, dễ trích dẫn trong báo cáo.
- Cấu trúc dữ liệu quan hệ tự nhiên, gồm các bảng collision, vehicle và casualty.
- Dữ liệu đủ lớn để phân tích thống kê, xu hướng và tương quan.
- Có nhiều chiều phân tích: thời gian, điều kiện đường, thời tiết, ánh sáng, loại phương tiện, nhóm tuổi, mức độ thương vong.
- Chủ đề có ý nghĩa xã hội, dễ rút ra insight và khuyến nghị.
- Có thể thu hẹp phạm vi còn 3-5 năm gần nhất để phù hợp báo cáo 24 trang.

## 5. Bài toán phân tích chung

> Phân tích các yếu tố về thời gian, điều kiện đường sá, phương tiện và đặc điểm người tham gia giao thông ảnh hưởng đến mức độ nghiêm trọng của tai nạn đường bộ tại Vương quốc Anh.

Bài toán này đủ gọn để triển khai trong báo cáo giới hạn 24 trang, nhưng vẫn đủ sâu để dùng mô hình dữ liệu quan hệ và xây dashboard Power BI có nhiều góc nhìn.

## 6. Mục tiêu phân tích con

### Mục tiêu 1: Xu hướng tai nạn theo thời gian

- Số vụ tai nạn và số người thương vong thay đổi như thế nào theo năm, tháng, ngày trong tuần và giờ trong ngày?
- Có khung giờ, ngày hoặc tháng nào có rủi ro cao bất thường không?

### Mục tiêu 2: Điều kiện môi trường và hạ tầng

- Mức độ nghiêm trọng của tai nạn thay đổi như thế nào theo loại đường, tốc độ giới hạn, thời tiết và điều kiện ánh sáng?
- Điều kiện nào thường đi kèm với tai nạn nghiêm trọng?

### Mục tiêu 3: Phương tiện và nhóm người tham gia giao thông

- Loại phương tiện nào xuất hiện nhiều trong các vụ tai nạn nghiêm trọng?
- Nhóm tuổi, giới tính hoặc vai trò tham gia giao thông nào có rủi ro thương vong cao?

### Mục tiêu 4: Tương quan với mức độ nghiêm trọng

- Các yếu tố như thời tiết xấu, ánh sáng kém, loại đường, tốc độ giới hạn và loại phương tiện có liên quan thế nào đến accident severity/casualty severity?
- Có thể nhận diện các nhóm tình huống rủi ro cao để đề xuất khuyến nghị an toàn giao thông không?

## 7. Cấu trúc dữ liệu đề xuất

| Bảng | Vai trò | Ý nghĩa |
| :--- | :--- | :--- |
| `Collisions` / `Accidents` | Fact chính | Một dòng là một vụ va chạm/tai nạn; chứa ngày, giờ, vị trí, loại đường, thời tiết, ánh sáng, speed limit và accident severity. |
| `Vehicles` | Fact phụ / bảng chi tiết | Các phương tiện liên quan đến từng vụ tai nạn; chứa loại xe, tuổi xe, hướng đi, thao tác, điểm va chạm. |
| `Casualties` | Fact phụ / bảng chi tiết | Người bị thương/vong trong từng vụ tai nạn; chứa casualty severity, tuổi, giới tính, vai trò tham gia giao thông. |
| `Lookup tables` | Dimension | Giải mã các mã phân loại như road type, weather condition, light condition, vehicle type, casualty class, severity. |
| `Calendar` | Dimension | Tự tạo trong Power BI để phân tích theo năm, quý, tháng, tuần và ngày trong tuần. |

## 8. Relationship dự kiến

- `Collisions[accident_index]` 1-n `Vehicles[accident_index]`
- `Collisions[accident_index]` 1-n `Casualties[accident_index]`
- `Calendar[Date]` 1-n `Collisions[date]`
- Lookup tables 1-n tới `Collisions`, `Vehicles`, `Casualties` qua các cột mã phân loại.

## 9. Phạm vi dữ liệu nên dùng

Không nên tải và dùng toàn bộ dữ liệu từ 1979 đến năm mới nhất vì dung lượng quá lớn và vượt nhu cầu báo cáo.

Khuyến nghị dùng:

- **Latest 5 years of data** nếu muốn phân tích xu hướng đủ rộng.
- Hoặc **latest full validated year** nếu muốn nhẹ hơn và dễ làm nhanh.

Với đồ án này, nên chọn **Latest 5 years of data** gồm 3 file:

- Road Safety Data - Collisions - last 5 years
- Road Safety Data - Vehicles - last 5 years
- Road Safety Data - Casualties - last 5 years

Ba file này đủ mạnh để xây mô hình quan hệ và phân tích, nhưng vẫn gọn hơn rất nhiều so với bộ dữ liệu đầy đủ từ năm 1979.

## 10. Hướng dẫn tải dữ liệu thô

### Cách 1: Tải thủ công từ GOV.UK

1. Mở trang chính thức:
   - https://www.gov.uk/government/statistical-data-sets/road-safety-open-data
2. Kéo xuống phần **Additional data files**.
3. Tìm mục **Latest 5 years of data**.
4. Tải 3 file CSV:
   - `Road Safety Data - Collisions - last 5 years`
   - `Road Safety Data - Vehicles - last 5 years`
   - `Road Safety Data - Casualties - last 5 years`
5. Kéo lên phần **Guidance and documentation**.
6. Tải thêm file:
   - `Open dataset data guide`
7. Tạo thư mục trong project:
   - `data/raw/uk_road_safety`
8. Lưu 4 file vừa tải vào thư mục đó.

### Cách 2: Tải dữ liệu mới nhất theo từng năm

Nếu máy yếu hoặc muốn làm nhẹ hơn:

1. Vào cùng trang GOV.UK ở trên.
2. Tại phần **Latest full year of final validated data**, tải 3 file của năm mới nhất:
   - `Road Safety Data - Collisions - 2024`
   - `Road Safety Data - Vehicles - 2024`
   - `Road Safety Data - Casualties - 2024`
3. Tải thêm `Open dataset data guide`.
4. Lưu vào:
   - `data/raw/uk_road_safety`

Cách này nhẹ hơn, phù hợp nếu nhóm ưu tiên hoàn thành mô hình và dashboard nhanh. Tuy nhiên, phân tích xu hướng theo năm sẽ yếu hơn so với phương án 5 năm.

### Cách 3: Tải bằng PowerShell

Mở PowerShell tại thư mục project và chạy:

```powershell
New-Item -ItemType Directory -Force .\data\raw\uk_road_safety
```

Sau đó vào trang GOV.UK, bấm chuột phải vào từng link CSV trong mục **Latest 5 years of data**, chọn **Copy link address**, rồi tải bằng lệnh:

```powershell
Invoke-WebRequest -Uri "PASTE_LINK_COLLISIONS_CSV_HERE" -OutFile ".\data\raw\uk_road_safety\collisions_last_5_years.csv"
Invoke-WebRequest -Uri "PASTE_LINK_VEHICLES_CSV_HERE" -OutFile ".\data\raw\uk_road_safety\vehicles_last_5_years.csv"
Invoke-WebRequest -Uri "PASTE_LINK_CASUALTIES_CSV_HERE" -OutFile ".\data\raw\uk_road_safety\casualties_last_5_years.csv"
Invoke-WebRequest -Uri "PASTE_LINK_DATA_GUIDE_HERE" -OutFile ".\data\raw\uk_road_safety\road_safety_open_dataset_data_guide.xlsx"
```

Không nên hard-code link trong báo cáo vì GOV.UK có thể cập nhật file theo năm. Trong báo cáo, trích dẫn trang chính thức của GOV.UK là đủ.

## 11. Gợi ý import vào Power BI

1. Mở Power BI Desktop.
2. Chọn **Get data > Text/CSV**.
3. Import lần lượt:
   - `collisions_last_5_years.csv`
   - `vehicles_last_5_years.csv`
   - `casualties_last_5_years.csv`
4. Trong Power Query:
   - Đổi cột `date` sang kiểu `Date`.
   - Đổi các cột số như `number_of_vehicles`, `number_of_casualties`, `speed_limit`, `age_of_casualty` sang numeric.
   - Kiểm tra các mã `-1`, `99`, hoặc giá trị tương tự theo data guide vì chúng thường biểu diễn unknown/missing.
5. Tạo bảng `Calendar`.
6. Thiết lập relationship:
   - `Collisions[accident_index]` tới `Vehicles[accident_index]`
   - `Collisions[accident_index]` tới `Casualties[accident_index]`
   - `Calendar[Date]` tới `Collisions[date]`
7. Tạo các measure cơ bản:
   - `Total Collisions = COUNTROWS(Collisions)`
   - `Total Casualties = COUNTROWS(Casualties)`
   - `Total Vehicles = COUNTROWS(Vehicles)`
   - `Fatal Collisions`
   - `Serious Collisions`
   - `Slight Collisions`
   - `Fatal/Serious Rate`

## 12. Dashboard đề xuất

### Trang 1: Tổng quan an toàn giao thông

- KPI tổng số tai nạn, tổng số thương vong, số vụ fatal/serious/slight.
- Line chart số vụ tai nạn theo tháng/năm.
- Column chart số vụ tai nạn theo ngày trong tuần hoặc giờ trong ngày.

### Trang 2: Điều kiện tai nạn

- Bar chart severity theo loại đường.
- Matrix severity theo thời tiết và điều kiện ánh sáng.
- Heatmap tai nạn theo giờ trong ngày và ngày trong tuần.

### Trang 3: Phương tiện và nạn nhân

- Bar chart số vụ theo loại phương tiện.
- Stacked chart casualty severity theo nhóm tuổi.
- Matrix loại phương tiện và casualty severity.

### Trang 4: Nhận diện tình huống rủi ro cao

- Scatter hoặc bubble chart giữa speed limit, số phương tiện, số thương vong và severity.
- Top nhóm điều kiện có tỷ lệ serious/fatal cao.
- Kết luận và khuyến nghị an toàn giao thông.

## 13. Kết luận

Dataset được chọn để triển khai là **UK Road Safety / STATS19 Road Safety Open Data**. Đây là dataset đủ mạnh, có tính quan hệ rõ, nguồn chính thức, không trùng với đề tài Brazilian Ecommerce, và phù hợp để phân tích trong phạm vi báo cáo 24 trang.

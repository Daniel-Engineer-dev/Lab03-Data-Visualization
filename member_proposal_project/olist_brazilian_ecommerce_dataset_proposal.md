# PHIẾU ĐỀ XUẤT BỘ DỮ LIỆU ĐỒ ÁN
## Đồ án Lab 03: Trực quan hóa dữ liệu bằng Power BI

## 0. Kết luận lựa chọn dataset

**Dataset đề xuất:** Brazilian E-Commerce Public Dataset by Olist.

Sau khi đối chiếu với tiêu chí phê duyệt của đồ án, đây là lựa chọn phù hợp nhất vì:

- Dữ liệu có tính thực tế cao: đây là dữ liệu thương mại điện tử thật của Olist tại Brazil, đã được ẩn danh.
- Có cấu trúc quan hệ rõ ràng với 9 file CSV, gồm bảng đơn hàng, chi tiết sản phẩm trong đơn, khách hàng, người bán, sản phẩm, thanh toán, đánh giá và địa lý.
- Bảng giao dịch chính có hơn 100,000 dòng, đủ lớn để phân tích xu hướng, phân nhóm, xếp hạng và tương quan.
- Có nhiều trường ngày tháng, số đo định lượng và trường phân loại, phù hợp để làm dashboard Power BI có slicer/filter/storyboard.
- Dữ liệu đủ phong phú để chia thành 4 mục tiêu phân tích độc lập cho 4 thành viên nhưng vẫn thống nhất trong một chủ đề chung: hiệu quả kinh doanh, sản phẩm, khách hàng/người bán và vận hành giao hàng.
- Mức độ khuyết dữ liệu ở các khóa liên kết và số đo chính thấp; các cột thiếu nhiều hơn chủ yếu là nội dung bình luận review hoặc mốc thời gian của đơn hàng chưa giao/hủy, có thể xử lý hợp lý bằng Power Query.

### So sánh nhanh với các ứng viên khác trên Kaggle

| Dataset | Nhận xét | Lý do không ưu tiên |
| :--- | :--- | :--- |
| **Brazilian E-Commerce Public Dataset by Olist** | 9 bảng CSV, dữ liệu thật, có đơn hàng, sản phẩm, khách hàng, seller, thanh toán, vận chuyển, review, địa lý. | **Được chọn** vì cân bằng tốt giữa tính thực tế, độ phong phú và mức độ dễ triển khai trong Power BI. |
| Instacart Online Grocery Basket Analysis | Nhiều bảng, dữ liệu lớn, phù hợp phân tích hành vi mua lặp lại. | Dung lượng lớn hơn nhiều, thiên về machine learning/market basket; thiếu doanh thu, thanh toán, review, giao vận nên khó đáp ứng đủ 4 hướng phân tích của bài. |
| Maven Market Datasets | Nhiều bảng, khá dễ làm dashboard bán lẻ. | Nguồn và license trên Kaggle không rõ bằng Olist, dữ liệu có tính bài tập/giả lập cao hơn, kém thuyết phục hơn khi yêu cầu dataset thực tế. |

---

## 1. Thông tin thành viên đề xuất

- **Họ và Tên**: ..............................................................
- **MSSV**: ...................................................................
- **Vai trò trong nhóm**: Đề xuất và đánh giá bộ dữ liệu; hỗ trợ thiết kế data model và mục tiêu phân tích.

---

## 2. Thông tin chung về Bộ dữ liệu (Dataset Overview)

- **Tên bộ dữ liệu**: Brazilian E-Commerce Public Dataset by Olist.
- **Lĩnh vực/Chủ đề phân tích**: Thương mại điện tử, bán lẻ trực tuyến, vận hành giao hàng, hành vi khách hàng và hiệu quả người bán.
- **Nguồn cung cấp (Đường dẫn tải/Link)**: https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce
- **Nhà cung cấp dữ liệu**: Olist.
- **Giấy phép**: CC BY-NC-SA 4.0.
- **Định dạng tệp tin**: CSV.
- **Tổng dung lượng & số lượng dòng**:
  - Tổng dung lượng thô khoảng 126 MB.
  - Gồm 9 file CSV.
  - Tổng số dòng các bảng khoảng hơn 1.5 triệu dòng nếu tính cả bảng geolocation.
  - Bảng giao dịch chính `olist_order_items_dataset.csv` có khoảng 112,650 dòng.
  - Bảng đơn hàng `olist_orders_dataset.csv` có khoảng 99,441 đơn hàng, giai đoạn 2016-2018.

### Ý nghĩa thực tế của bài toán

Olist là nền tảng marketplace kết nối các doanh nghiệp nhỏ tại Brazil với người mua trên nhiều kênh bán hàng. Bộ dữ liệu cho phép nhóm phân tích một chuỗi thương mại điện tử khá đầy đủ: khách đặt hàng, seller xử lý đơn, sản phẩm được giao, khách thanh toán và sau đó đánh giá trải nghiệm. Đây là bài toán gần với vận hành kinh doanh thực tế, có thể rút ra insight về doanh thu, danh mục sản phẩm, phân bố khách hàng/seller, chất lượng giao hàng và mức độ hài lòng.

---

## 3. Cấu trúc Mô hình Quan hệ Đề xuất

### 3.1. Danh sách các bảng dữ liệu

| Tên Bảng | Số lượng dòng ước tính | Vai trò (Fact / Dimension) | Ý nghĩa của bảng |
| :--- | ---: | :--- | :--- |
| `olist_order_items_dataset.csv` | 112,650 | Fact Table chính | Chi tiết từng sản phẩm trong đơn hàng; chứa `order_id`, `order_item_id`, `product_id`, `seller_id`, `price`, `freight_value`, `shipping_limit_date`. Đây là bảng trung tâm để tính doanh thu sản phẩm, phí vận chuyển, số lượng item và hiệu quả seller. |
| `olist_orders_dataset.csv` | 99,441 | Transaction Header / Dimension đơn hàng | Thông tin cấp đơn hàng: `order_id`, `customer_id`, trạng thái đơn, ngày mua, ngày duyệt, ngày giao cho đơn vị vận chuyển, ngày giao thực tế và ngày giao dự kiến. |
| `olist_order_payments_dataset.csv` | 103,886 | Fact phụ / Payment bridge | Thông tin thanh toán theo đơn hàng: `payment_type`, `payment_installments`, `payment_value`. Có thể aggregate về cấp `order_id` để tránh quan hệ nhiều-nhiều. |
| `olist_order_reviews_dataset.csv` | 99,224 | Fact phụ / Dimension trải nghiệm | Điểm đánh giá và nội dung review của khách hàng theo `order_id`, gồm `review_score`, ngày tạo review và ngày trả lời review. Có thể dùng để phân tích hài lòng khách hàng. |
| `olist_customers_dataset.csv` | 99,441 | Dimension | Thông tin khách hàng đã ẩn danh: `customer_id`, `customer_unique_id`, zip code prefix, thành phố, bang. Dùng để phân tích địa lý và hành vi mua lặp lại. |
| `olist_products_dataset.csv` | 32,951 | Dimension | Danh mục sản phẩm và đặc trưng sản phẩm: `product_id`, `product_category_name`, độ dài tên/mô tả, số ảnh, cân nặng, kích thước. |
| `olist_sellers_dataset.csv` | 3,095 | Dimension | Thông tin người bán: `seller_id`, zip code prefix, thành phố, bang. Dùng để xếp hạng seller và phân tích vận hành theo địa lý. |
| `olist_geolocation_dataset.csv` | 1,000,163 | Dimension địa lý / Lookup | Tọa độ latitude/longitude theo zip code prefix, thành phố và bang tại Brazil. Nên tổng hợp thành bảng zip code duy nhất trước khi liên kết để tránh many-to-many. |
| `product_category_name_translation.csv` | 71 | Dimension lookup | Bảng dịch tên danh mục sản phẩm từ tiếng Bồ Đào Nha sang tiếng Anh, giúp dashboard dễ đọc hơn. |

### 3.2. Dự kiến sơ đồ liên kết giữa các bảng (Schema Keys)

Đề xuất mô hình dạng star/snowflake schema, lấy `olist_order_items_dataset.csv` làm fact chính ở cấp độ từng item trong đơn hàng.

- **Customers** liên kết với **Orders** qua khóa `customer_id`: quan hệ `1:n`.
- **Orders** liên kết với **Order Items** qua khóa `order_id`: quan hệ `1:n`.
- **Products** liên kết với **Order Items** qua khóa `product_id`: quan hệ `1:n`.
- **Sellers** liên kết với **Order Items** qua khóa `seller_id`: quan hệ `1:n`.
- **Orders** liên kết với **Order Payments** qua khóa `order_id`: quan hệ `1:n`; trong Power BI nên tạo bảng thanh toán đã aggregate theo `order_id` nếu cần phân tích ở cấp đơn hàng.
- **Orders** liên kết với **Order Reviews** qua khóa `order_id`: quan hệ gần `1:1`, nhưng cần kiểm tra duplicate review; nếu có nhiều review trên một đơn thì aggregate về điểm review trung bình hoặc review mới nhất.
- **Products** liên kết với **Category Translation** qua khóa `product_category_name`: quan hệ `n:1`.
- **Customers/Sellers** có thể liên kết với **Geolocation** qua `customer_zip_code_prefix` hoặc `seller_zip_code_prefix`; nên tạo bảng `Dim_GeolocationZip` đã loại trùng theo zip prefix, city, state trước khi liên kết.
- Nên tạo thêm bảng **Calendar/Date** trong Power BI từ `order_purchase_timestamp`, sau đó liên kết với **Orders** theo ngày mua hàng để phân tích theo năm, quý, tháng, tuần.

### 3.3. Các measure/DAX dự kiến

- `Total Revenue = SUM(OrderItems[price])`
- `Total Freight = SUM(OrderItems[freight_value])`
- `Total Order Value = [Total Revenue] + [Total Freight]`
- `Total Orders = DISTINCTCOUNT(Orders[order_id])`
- `Total Items = COUNTROWS(OrderItems)`
- `Average Order Value = DIVIDE([Total Order Value], [Total Orders])`
- `Average Review Score = AVERAGE(OrderReviews[review_score])`
- `Delivery Days = DATEDIFF(Orders[order_purchase_timestamp], Orders[order_delivered_customer_date], DAY)`
- `Delay Days = DATEDIFF(Orders[order_estimated_delivery_date], Orders[order_delivered_customer_date], DAY)`
- `On-time Delivery Rate = DIVIDE(COUNTROWS(FILTER(Orders, Orders[Delay Days] <= 0)), COUNTROWS(Orders))`

---

## 4. Bảng tự đánh giá tiêu chí phê duyệt (Feasibility Checklist)

- [x] **Tính quan hệ**: Có 9 bảng CSV và thiết lập được nhiều quan hệ `1:n` rõ ràng, không phải bảng phẳng đơn lẻ.
- [x] **Độ lớn dữ liệu**: Bảng fact chính `olist_order_items_dataset.csv` có trên 1,000 dòng, thực tế khoảng 112,650 dòng.
- [x] **Chiều thời gian**: Có nhiều cột ngày/thời gian như `order_purchase_timestamp`, `order_approved_at`, `order_delivered_carrier_date`, `order_delivered_customer_date`, `order_estimated_delivery_date`, `shipping_limit_date`.
- [x] **Số đo lường**: Có nhiều cột định lượng như `price`, `freight_value`, `payment_value`, `payment_installments`, `review_score`, `product_weight_g`, `product_length_cm`, `product_height_cm`, `product_width_cm`.
- [x] **Trường phân loại**: Có `order_status`, `payment_type`, `product_category_name`, `customer_city`, `customer_state`, `seller_city`, `seller_state`.
- [x] **Khả năng làm sạch**: Dữ liệu ở dạng CSV, schema rõ, có thể xử lý bằng Power Query: đổi kiểu dữ liệu, loại trùng geolocation, aggregate payment/review, xử lý null ngày giao hàng.
- [x] **Bảo mật**: Dữ liệu thương mại thật nhưng đã được ẩn danh; không chứa thông tin nhạy cảm như tên thật, số điện thoại, CCCD hay số thẻ tín dụng.
- [x] **Nguồn gốc rõ ràng**: Dataset công khai trên Kaggle, nhà cung cấp là Olist.

---

## 5. Phác thảo 4 Mục tiêu phân tích dự kiến cho nhóm

### 1. Mục tiêu 1 (Thành viên A - Thời gian & Chỉ số vĩ mô)

- **Các cột dữ liệu sử dụng**:
  - `Orders[order_purchase_timestamp]`
  - `Orders[order_status]`
  - `OrderItems[price]`
  - `OrderItems[freight_value]`
  - `Payments[payment_value]`
  - `Calendar[Year]`, `Calendar[Quarter]`, `Calendar[Month]`
- **Câu hỏi phân tích dự kiến**:
  - Doanh thu, số đơn hàng và giá trị đơn hàng trung bình thay đổi như thế nào theo tháng/quý/năm trong giai đoạn 2016-2018?
  - Có mùa cao điểm hoặc giai đoạn sụt giảm rõ rệt không?
  - Tỷ lệ đơn giao thành công, hủy hoặc không hoàn tất thay đổi như thế nào theo thời gian?
- **Biểu đồ đề xuất**:
  - Line chart doanh thu theo tháng.
  - Clustered column chart số đơn theo tháng/quý.
  - KPI cards: tổng doanh thu, tổng đơn, AOV, tổng phí vận chuyển, điểm review trung bình.
  - Area/column chart tỷ trọng trạng thái đơn hàng theo thời gian.

### 2. Mục tiêu 2 (Thành viên B - Phân loại & Danh mục)

- **Các cột dữ liệu sử dụng**:
  - `Products[product_category_name]`
  - `CategoryTranslation[product_category_name_english]`
  - `OrderItems[price]`
  - `OrderItems[freight_value]`
  - `OrderItems[product_id]`
  - `Orders[order_status]`
- **Câu hỏi phân tích dự kiến**:
  - Danh mục sản phẩm nào tạo doanh thu cao nhất và danh mục nào có số lượng bán cao nhất?
  - Cơ cấu doanh thu giữa các danh mục có tập trung vào một vài nhóm sản phẩm hay phân tán?
  - Danh mục nào có phí vận chuyển trung bình cao hoặc điểm review thấp, cần chú ý về chất lượng/vận hành?
- **Biểu đồ đề xuất**:
  - Bar chart top 10 danh mục theo doanh thu.
  - Treemap cơ cấu doanh thu theo danh mục.
  - Donut chart tỷ trọng đơn hàng theo nhóm danh mục chính.
  - Matrix so sánh doanh thu, số đơn, phí vận chuyển trung bình, review score theo danh mục.

### 3. Mục tiêu 3 (Thành viên C - Phân khúc & Hành vi Chủ thể)

- **Các cột dữ liệu sử dụng**:
  - `Customers[customer_unique_id]`
  - `Customers[customer_city]`, `Customers[customer_state]`
  - `Sellers[seller_id]`, `Sellers[seller_city]`, `Sellers[seller_state]`
  - `Orders[order_id]`, `Orders[order_purchase_timestamp]`
  - `OrderItems[price]`, `OrderItems[freight_value]`
  - `Payments[payment_type]`, `Payments[payment_installments]`
- **Câu hỏi phân tích dự kiến**:
  - Khách hàng theo bang/thành phố nào đóng góp nhiều doanh thu và số đơn nhất?
  - Có bao nhiêu khách hàng mua lặp lại, nhóm khách hàng giá trị cao có đặc điểm gì?
  - Seller nào có doanh thu/số đơn cao nhất và seller nào có hiệu quả giao hàng hoặc review tốt nhất?
  - Phương thức thanh toán và số kỳ trả góp khác nhau như thế nào theo nhóm khách hàng/khu vực?
- **Biểu đồ đề xuất**:
  - Map hoặc filled map doanh thu/số đơn theo bang.
  - Scatter plot phân khúc khách hàng theo frequency và monetary value.
  - Matrix top customers/sellers theo doanh thu, số đơn, review score.
  - Stacked bar chart phương thức thanh toán theo bang hoặc phân khúc khách hàng.

### 4. Mục tiêu 4 (Thành viên D - Tương quan & Hiệu quả Vận hành)

- **Các cột dữ liệu sử dụng**:
  - `Orders[order_purchase_timestamp]`
  - `Orders[order_delivered_customer_date]`
  - `Orders[order_estimated_delivery_date]`
  - `OrderItems[freight_value]`
  - `OrderItems[price]`
  - `Products[product_weight_g]`, `Products[product_length_cm]`, `Products[product_height_cm]`, `Products[product_width_cm]`
  - `Reviews[review_score]`
  - `Customers[customer_state]`, `Sellers[seller_state]`
- **Câu hỏi phân tích dự kiến**:
  - Thời gian giao hàng thực tế có ảnh hưởng đến điểm review của khách hàng không?
  - Phí vận chuyển có tương quan với khối lượng/kích thước sản phẩm hoặc khoảng cách địa lý không?
  - Những bang hoặc tuyến seller-customer nào có nguy cơ giao trễ cao?
  - Đơn hàng có phí vận chuyển cao hoặc giao trễ có làm giảm mức độ hài lòng không?
- **Biểu đồ đề xuất**:
  - Scatter chart: `Delivery Days` hoặc `Delay Days` so với `review_score`.
  - Scatter chart: `freight_value` so với `product_weight_g` hoặc `order_value`.
  - Waterfall chart phân rã tổng giá trị đơn hàng thành giá sản phẩm và phí vận chuyển.
  - Heatmap/matrix tỷ lệ giao trễ theo bang khách hàng và bang seller.

---

## 6. Thách thức dự kiến & Các bước xử lý trên Power Query

### Thách thức của dữ liệu

- Một đơn hàng có thể có nhiều item, mỗi item có thể do seller khác nhau xử lý. Vì vậy cần thống nhất rõ granularity của fact chính là **một dòng item trong đơn hàng**.
- Bảng `order_payments` có thể có nhiều dòng cho một `order_id` nếu đơn hàng dùng nhiều phương thức thanh toán hoặc nhiều lần thanh toán. Nếu đưa trực tiếp vào model có thể làm sai tổng doanh thu khi join với `order_items`.
- Bảng `order_reviews` có thể có duplicate hoặc nhiều review cho một đơn hàng. Cần kiểm tra và aggregate trước khi nối vào model.
- Bảng `geolocation` có nhiều dòng trùng zip code prefix và tọa độ; nếu liên kết trực tiếp có thể tạo quan hệ nhiều-nhiều và làm phình dữ liệu.
- Một số cột ngày giao hàng bị null đối với đơn chưa giao, đơn hủy hoặc đơn không hoàn tất. Đây không phải lỗi dữ liệu nghiêm trọng nhưng cần xử lý khi tính `Delivery Days` và `Delay Days`.
- Một số sản phẩm thiếu danh mục hoặc thông tin kích thước/cân nặng; tỷ lệ này nhỏ và có thể xử lý bằng nhóm `Unknown` hoặc loại khỏi phân tích tương quan kích thước.
- Cột bình luận review có thể trống nhiều; vì đồ án Power BI tập trung trực quan hóa, nhóm có thể ưu tiên `review_score` thay vì NLP trên text review.

### Dự kiến các bước tiền xử lý chính

1. Import 9 file CSV vào Power BI Desktop.
2. Chuẩn hóa kiểu dữ liệu:
   - Chuyển các cột timestamp sang `Date/DateTime`.
   - Chuyển `price`, `freight_value`, `payment_value`, `review_score`, thông số kích thước sang numeric.
3. Tạo bảng `Calendar` từ khoảng ngày của `order_purchase_timestamp`.
4. Tạo bảng `Fact_OrderItems` từ `olist_order_items_dataset.csv`, giữ các khóa và số đo chính.
5. Tạo bảng `Dim_Orders` từ `olist_orders_dataset.csv`, thêm các cột:
   - `Purchase Date`
   - `Delivery Days`
   - `Delay Days`
   - `Is Delayed`
   - `Is Delivered`
6. Aggregate `olist_order_payments_dataset.csv` theo `order_id`:
   - Tổng `payment_value`.
   - Số kỳ trả góp lớn nhất hoặc trung bình.
   - Phương thức thanh toán chính.
7. Aggregate `olist_order_reviews_dataset.csv` theo `order_id`:
   - Điểm review trung bình hoặc review mới nhất.
   - Số lượng review trên mỗi đơn.
8. Làm sạch `olist_products_dataset.csv`:
   - Gộp với `product_category_name_translation.csv`.
   - Thay category rỗng bằng `Unknown`.
   - Tạo cột thể tích sản phẩm nếu cần: `length * height * width`.
9. Làm sạch `olist_geolocation_dataset.csv`:
   - Loại trùng theo `geolocation_zip_code_prefix`, `city`, `state`.
   - Có thể lấy trung bình latitude/longitude theo zip prefix để tạo `Dim_GeolocationZip`.
10. Thiết lập relationship trong Power BI:
    - Ưu tiên quan hệ `1:n`, single direction từ dimension sang fact.
    - Tránh join trực tiếp các bảng fact phụ với fact chính nếu chưa aggregate.
11. Tạo measure DAX phục vụ dashboard:
    - Doanh thu, số đơn, AOV, phí vận chuyển, tỷ lệ giao trễ, điểm review trung bình.
12. Kiểm tra chất lượng sau model:
    - So sánh tổng số đơn, tổng doanh thu, số item trước/sau khi tạo relationship.
    - Kiểm tra các filter/slicer không làm double-count doanh thu.

---

## 7. Đề xuất storyboard dashboard

### Trang 1: Executive Overview

- KPI cards: tổng doanh thu, tổng đơn, tổng item, AOV, phí vận chuyển, điểm review trung bình, tỷ lệ giao trễ.
- Line chart doanh thu theo tháng.
- Bar chart top danh mục theo doanh thu.
- Slicer: năm, tháng, bang khách hàng, danh mục sản phẩm, trạng thái đơn hàng.

### Trang 2: Product & Category Performance

- Treemap doanh thu theo category.
- Matrix category với doanh thu, số đơn, phí vận chuyển trung bình, review score.
- Top/bottom category theo review score hoặc tỷ lệ giao trễ.

### Trang 3: Customer, Seller & Geography

- Map doanh thu/số đơn theo bang khách hàng.
- Bar chart top seller theo doanh thu.
- Scatter phân khúc khách hàng theo số lần mua và tổng chi tiêu.
- Slicer theo bang seller/customer.

### Trang 4: Delivery & Satisfaction

- Scatter `Delivery Days` vs `Review Score`.
- Matrix tỷ lệ giao trễ theo bang khách hàng và bang seller.
- Bar chart phí vận chuyển trung bình theo category hoặc bang.
- Waterfall/chart phân tích order value và freight.

---

## 8. Nguồn tham khảo

- Kaggle - Brazilian E-Commerce Public Dataset by Olist: https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce
- Kaggle API metadata: https://www.kaggle.com/api/v1/datasets/view/olistbr/brazilian-ecommerce
- Kaggle API file list: https://www.kaggle.com/api/v1/datasets/list/olistbr/brazilian-ecommerce
- Olist website: https://www.olist.com/

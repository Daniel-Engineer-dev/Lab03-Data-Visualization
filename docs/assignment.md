# PHÂN CÔNG CÔNG VIỆC NHÓM 15

## Lab 03: Trực quan hóa dữ liệu bằng Power BI

Kế hoạch gồm hai giai đoạn:

- **Giai đoạn 1 - Dashboard và báo cáo:** 7 ngày, từ **14/06/2026 đến 20/06/2026**.
- **Giai đoạn 2 - Video thuyết trình:** 3 ngày, từ **21/06/2026 đến 23/06/2026**.

Các bước trong Giai đoạn 1 phải được thực hiện tuần tự. Nhóm chỉ bắt đầu vẽ biểu đồ sau khi dữ liệu sạch và Data Model đã được bàn giao; dashboard tổng chỉ được ghép sau khi bốn file Power BI cá nhân hoàn thành.

---

## 1. Thành viên và nhiệm vụ chính

| Thành viên             | MSSV       | Mục tiêu phân tích cá nhân       | Nhiệm vụ bổ sung                                           |
| :--------------------- | :--------- | :------------------------------- | :--------------------------------------------------------- |
| **Lê Lâm Trí Đức**     | `23120237` | Tổng quan và xu hướng thời gian  | Dashboard tổng, hoàn thiện Mục 4.5, Mục 5 và build báo cáo |
| **Hoàng Quốc Việt**    | `23120189` | Điều kiện đường sá và môi trường | Dashboard tổng, slicer và kiểm tra tương tác               |
| **Nguyễn Lê Thế Vinh** | `23120190` | Phương tiện và người lái         | Data Model, tiền xử lý và hoàn thành Mục 2                 |
| **Phạm Quang Vinh**    | `23120202` | Người thương vong và nhóm rủi ro | Tiền xử lý, giải mã dữ liệu và hoàn thành Mục 2            |

Mỗi thành viên chịu trách nhiệm tạo **một file Power BI cá nhân**, gồm **4 biểu đồ chính** và phần phân tích cho mục tiêu được giao.

---

## 2. Giai đoạn 1: Dashboard và Báo cáo

### Bước 1 - Xây dựng mô hình và tiền xử lý dữ liệu

**Thời gian:** 14/06 đến hết 16/06  
**Phụ trách:** Nguyễn Lê Thế Vinh, Phạm Quang Vinh

> [!IMPORTANT]
> **Yêu cầu bắt buộc:** Toàn bộ công việc làm sạch (clean) và tiền xử lý dữ liệu phải được thực hiện trực tiếp bằng công cụ **Power BI** (thông qua Power Query). Tuyệt đối không dùng các công cụ ngoài (như Python, R, Excel,...) để clean trước khi đưa vào Power BI.

#### Công việc

- Import ba bảng `Collisions`, `Vehicles` và `Casualties`.
- Chuẩn hóa kiểu dữ liệu và xử lý các mã `Unknown`, `Not applicable` hoặc giá trị thiếu.
- Giải mã các trường cần dùng dựa trên STATS19 Data Guide.
- Tạo bảng `Calendar` và các trường thời gian cần thiết.
- Thiết lập và kiểm tra quan hệ giữa các bảng.
- Chuẩn bị các measure dùng chung cho bốn thành viên.
- Kiểm tra số liệu sau tiền xử lý và ghi lại các bước đã thực hiện.
- Hoàn thành nội dung và ảnh Data Model cho **Mục 2** trong báo cáo.

#### Đầu ra bắt buộc

- Bộ dữ liệu sạch dùng chung, lưu trong `data/processed/`.
- File Power BI nền chứa dữ liệu sạch, Data Model và measure dùng chung.
- Ảnh chụp Data Model thực tế.
- **Mục 2 - Lựa chọn Dataset và Xây dựng Mô hình dữ liệu** hoàn chỉnh.
- Tài liệu ngắn mô tả các trường đã đổi tên, giải mã hoặc xử lý.

#### Điều kiện chuyển sang Bước 2

- Cả bốn thành viên mở được file Power BI nền.
- Quan hệ giữa các bảng hoạt động đúng.
- Các measure dùng chung trả về kết quả hợp lý.
- Không còn thay đổi lớn đối với cấu trúc dữ liệu sau khi bàn giao.

---

### Bước 2 - Vẽ biểu đồ và phân tích cá nhân

**Thời gian:** 17/06 đến hết 18/06  
**Phụ trách:** Cả bốn thành viên

Mỗi thành viên tạo một bản sao từ file Power BI nền, chỉ thực hiện mục tiêu được giao và không tự ý thay đổi Data Model dùng chung.

| Thành viên             | File bàn giao                  | Biểu đồ và nội dung phụ trách                                                                                                                                                                          |
| :--------------------- | :----------------------------- | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Lê Lâm Trí Đức**     | `powerbi/23120237_report.pbix` | 4 biểu đồ: Line (xu hướng theo năm), Heatmap (khung giờ & thứ), Column (số vụ theo tháng), Stacked Bar (tai nạn theo Đô thị/Nông thôn qua các năm); 3-4 nhận xét liên kết                              |
| **Hoàng Quốc Việt**    | `powerbi/23120189_report.pbix` | 4 biểu đồ: Stacked Bar (loại đường & mức độ), Heatmap Matrix (thời tiết & ánh sáng), Bar (giới hạn tốc độ), Clustered Column (mặt đường & khu vực); 3-4 nhận xét liên kết                              |
| **Nguyễn Lê Thế Vinh** | `powerbi/23120190_report.pbix` | 4 biểu đồ: Bar (loại phương tiện), Stacked Column (tuổi & giới tính người lái), Donut/Treemap (phương tiện theo Đô thị/Nông thôn), Line/Column (tỷ lệ tai nạn nặng theo nhóm tuổi); 3-4 nhận xét       |
| **Phạm Quang Vinh**    | `powerbi/23120202_report.pbix` | 4 biểu đồ: Stacked Bar (thương vong theo nhóm tuổi), Bar (theo vai trò tham gia), Clustered Column (thương vong theo tuổi & giới tính), 100% Stacked Column (mức độ thương vong theo vai trò); 3-4 nhận xét |

#### Công việc chung của mỗi thành viên

- Tạo đúng bốn biểu đồ đã được phân công.
- Đặt tiêu đề, nhãn, đơn vị và màu sắc dễ đọc.
- Kiểm tra số liệu và bộ lọc trên từng biểu đồ.
- Chụp một ảnh ghép chứa bốn biểu đồ.
- Viết 3-4 nhận xét liên kết ngắn gọn, có căn cứ trực tiếp từ số liệu.
- Hoàn thành phần phân tích tương ứng trong **Mục 4** báo cáo.

#### Đầu ra bắt buộc

- Bốn file `.pbix` cá nhân trong thư mục `powerbi/`.
- Bốn ảnh ghép biểu đồ cá nhân trong `report/images/`.
- Nội dung phân tích của bốn thành viên được điền vào **Mục 4**.

#### Điều kiện chuyển sang Bước 3

- Bốn file cá nhân mở được và sử dụng cùng một Data Model.
- Mỗi file có đủ bốn biểu đồ và nhận xét liên kết.
- Số liệu đã được ít nhất một thành viên khác kiểm tra chéo.

---

### Bước 3 - Xây dựng dashboard tổng hợp

**Thời gian:** 19/06  
**Phụ trách:** Lê Lâm Trí Đức, Hoàng Quốc Việt

#### Công việc

- Tổng hợp biểu đồ từ bốn file Power BI cá nhân.
- Bổ sung KPI tổng quan và các slicer cần thiết.
- Thiết lập tương tác chéo giữa biểu đồ và bộ lọc.
- Sắp xếp dashboard gọn, thống nhất và dễ theo dõi.
- Kiểm tra lại số liệu sau khi ghép dashboard.

#### Đầu ra bắt buộc

- File dashboard tổng hợp: `powerbi/group15_dashboard.pbix`.
- Ảnh chụp dashboard tổng hợp: `report/images/dashboard_overview.png`.
- Dashboard có KPI tổng quan, 16 biểu đồ chính và slicer phù hợp.

---

### Bước 4 - Hoàn thiện báo cáo

**Thời gian:** 20/06  
**Phụ trách chính:** Lê Lâm Trí Đức  
**Kiểm tra và duyệt:** Cả nhóm

#### Công việc

- Chèn ảnh dashboard tổng hợp vào **Mục 4.5**.
- Kiểm tra ảnh và nội dung phân tích của từng thành viên trong Mục 4.
- Tổng hợp các insight nổi bật từ dashboard.
- Hoàn thành **Mục 5** gồm kết luận, khuyến nghị, hạn chế và tài liệu tham khảo.
- Build PDF và kiểm tra lỗi trình bày.
- Kiểm tra báo cáo không vượt quá 24 trang.

#### Đầu ra bắt buộc

- **Mục 4** hoàn chỉnh, có ảnh dashboard tại Mục 4.5.
- **Mục 5** hoàn chỉnh và dựa trên kết quả phân tích thực tế.
- File `report/main.pdf` hoàn chỉnh, không vượt quá 24 trang.
- File dashboard tổng và bốn file Power BI cá nhân đã được kiểm tra.

---

## 3. Lịch bàn giao Giai đoạn 1

| Hạn chót          | Sản phẩm bàn giao                                               | Người phụ trách      |
| :---------------- | :-------------------------------------------------------------- | :------------------- |
| **16/06 - 23:59** | Dữ liệu sạch, Data Model, file Power BI nền và Mục 2 báo cáo    | Thế Vinh, Quang Vinh |
| **17/06 - 23:59** | Mỗi thành viên hoàn thành biểu đồ đầu tiên                       | Cả nhóm              |
| **18/06 - 23:59** | Bốn file `.pbix` cá nhân, 16 biểu đồ, ảnh ghép và nội dung Mục 4 | Cả nhóm              |
| **19/06 - 23:59** | Dashboard tổng hợp và ảnh `dashboard_overview.png`              | Đức, Việt            |
| **20/06 - 23:59** | Mục 4.5, Mục 5 và PDF hoàn chỉnh                                | Đức; cả nhóm duyệt   |

### Điều kiện hoàn thành Giai đoạn 1

- [ ] Bộ dữ liệu sạch và Data Model dùng chung đã được bàn giao.
- [ ] Mục 2 trong báo cáo đã hoàn chỉnh.
- [ ] Có đủ bốn file `.pbix` cá nhân.
- [ ] Mỗi thành viên có đúng bốn biểu đồ và 3-4 nhận xét liên kết.
- [ ] Mục 4 đã có đầy đủ ảnh và nội dung phân tích.
- [ ] Dashboard tổng có KPI, 16 biểu đồ chính và slicer.
- [ ] Ảnh dashboard tổng đã được chèn vào Mục 4.5.
- [ ] Mục 5 đã được hoàn thành từ kết quả thực tế.
- [ ] Báo cáo PDF build thành công và không vượt quá 24 trang.

---

## 4. Giai đoạn 2: Quay và hoàn thành Video

| Ngày      | Công việc chính                                                  | Người phụ trách                | Đầu ra bắt buộc                                  |
| :-------- | :--------------------------------------------------------------- | :----------------------------- | :----------------------------------------------- |
| **21/06** | Viết kịch bản, chia thời lượng và tập thuyết trình               | Cả nhóm                        | Kịch bản hoàn chỉnh, thống nhất thứ tự trình bày |
| **22/06** | Quay phần giới thiệu, Data Model, dashboard và phân tích cá nhân | Cả nhóm                        | Đủ video thô và bản ghi màn hình Power BI        |
| **23/06** | Dựng video, kiểm tra âm thanh và xuất bản cuối                   | Quang Vinh dựng; cả nhóm duyệt | Video hoàn chỉnh và file nộp bài                 |

### Phân chia nội dung video

| Thành viên             | Nội dung trình bày                                                      |
| :--------------------- | :---------------------------------------------------------------------- |
| **Lê Lâm Trí Đức**     | Giới thiệu đề tài, Data Model, dashboard tổng hợp và xu hướng thời gian |
| **Hoàng Quốc Việt**    | Quy trình tiền xử lý và phân tích điều kiện đường sá, môi trường        |
| **Nguyễn Lê Thế Vinh** | Tương tác dashboard và phân tích phương tiện, người lái                 |
| **Phạm Quang Vinh**    | Phân tích người thương vong, kết luận, khuyến nghị và tổng kết          |

---

## 5. Quy tắc phối hợp

- Mỗi ngày cập nhật tiến độ trước **22:00**.
- Chỉ sử dụng dữ liệu sạch và file Power BI nền đã được bàn giao ở Bước 1.
- Không tự ý thay đổi Data Model hoặc measure dùng chung.
- Mọi biểu đồ và insight phải được ít nhất một thành viên khác kiểm tra.
- Người phụ trách bước sau phải kiểm tra đầy đủ đầu ra của bước trước khi tiếp nhận.
- Sau ngày **20/06/2026**, chỉ sửa lỗi; không bổ sung mục tiêu hoặc biểu đồ mới.

---

## 6. Checklist bàn giao cuối cùng

- [ ] Bộ dữ liệu sạch trong `data/processed/`.
- [ ] File Power BI nền, bốn file cá nhân và dashboard tổng mở được.
- [ ] Báo cáo PDF hoàn chỉnh, không vượt quá 24 trang.
- [ ] Video có phần trình bày của cả bốn thành viên.
- [ ] Âm thanh video rõ ràng, không có đoạn thừa hoặc màn hình lỗi.
- [ ] Các file nộp bài được kiểm tra và đóng gói đầy đủ.

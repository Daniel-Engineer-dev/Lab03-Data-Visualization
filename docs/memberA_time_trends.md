# HƯỚNG DẪN DENEB: XU HƯỚNG THỜI GIAN (LÊ LÂM TRÍ ĐỨC)

Tài liệu này cung cấp mã JSON Vega-lite để vẽ 4 biểu đồ phân tích về **Xu hướng thời gian** dựa trên bảng mô tả `dataset_description.md`.
Màu sắc chủ đạo: **Blue (`#60A5FA`)**

> **LƯU Ý QUAN TRỌNG:** Phải kéo đúng tên cột từ các bảng tương ứng vào mục **Values** của Deneb visual trước khi dán mã JSON.

---

## 1. Biểu đồ 1: Số vụ va chạm theo năm và mức độ (Line Chart)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Calendar` > **`Year`**
- `Collisions` > **`collision_severity_label`**
- `Collisions` > **`Total Collisions`** (Measure)

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "mark": {
    "type": "line",
    "strokeWidth": 3,
    "point": {"filled": true}
  },
  "encoding": {
    "x": {
      "field": "Year",
      "type": "ordinal",
      "title": "Năm"
    },
    "y": {
      "field": "Total Collisions",
      "type": "quantitative",
      "title": "Tổng số vụ va chạm"
    },
    "color": {
      "field": "collision_severity_label",
      "type": "nominal",
      "title": "Mức độ nghiêm trọng",
      "scale": {
        "domain": ["Fatal", "Serious", "Slight"],
        "range": ["#EF4444", "#FBBF24", "#60A5FA"]
      }
    },
    "tooltip": [
      {"field": "Year", "title": "Năm"},
      {"field": "collision_severity_label", "title": "Mức độ"},
      {"field": "Total Collisions", "title": "Số vụ va chạm", "format": ","}
    ]
  }
}
```

---

## 2. Biểu đồ 2: Số vụ va chạm theo tháng (Column Chart)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Calendar` > **`Month Name`**
- `Calendar` > **`Month Number`** (Kéo vào Tooltip hoặc ẩn đi để sort, hoặc sort trực tiếp ở ngoài Power BI)
- `Collisions` > **`Total Collisions`** (Measure)

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "mark": {
    "type": "bar",
    "color": "#60A5FA",
    "cornerRadiusEnd": 4
  },
  "encoding": {
    "x": {
      "field": "Month Name",
      "type": "nominal",
      "title": "Tháng",
      "sort": {"field": "Month Number"}
    },
    "y": {
      "field": "Total Collisions",
      "type": "quantitative",
      "title": "Tổng số vụ va chạm"
    },
    "tooltip": [
      {"field": "Month Name", "title": "Tháng"},
      {"field": "Total Collisions", "title": "Số vụ", "format": ","}
    ]
  }
}
```

---

## 3. Biểu đồ 3: Mật độ va chạm theo Thứ và Giờ (Heatmap Matrix)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Collisions` > **`day_of_week_label`**
- `Collisions` > **`time`** (Sẽ trích xuất theo giờ)
- `Collisions` > **`Total Collisions`** (Measure)

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "mark": "rect",
  "encoding": {
    "y": {
      "field": "day_of_week_label",
      "type": "nominal",
      "title": "Thứ trong tuần",
      "sort": ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"]
    },
    "x": {
      "field": "time",
      "type": "ordinal",
      "timeUnit": "hours",
      "title": "Giờ trong ngày"
    },
    "color": {
      "field": "Total Collisions",
      "type": "quantitative",
      "title": "Số vụ va chạm",
      "scale": {"scheme": "blues"}
    },
    "tooltip": [
      {"field": "day_of_week_label", "title": "Thứ"},
      {"field": "time", "timeUnit": "hours", "title": "Giờ"},
      {"field": "Total Collisions", "title": "Số vụ va chạm", "format": ","}
    ]
  }
}
```

---

## 4. Biểu đồ 4: Số vụ va chạm theo năm và khu vực (Stacked Bar Chart)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Calendar` > **`Year`**
- `Collisions` > **`urban_or_rural_area_label`**
- `Collisions` > **`Total Collisions`** (Measure)

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "mark": {"type": "bar", "cornerRadiusEnd": 2},
  "encoding": {
    "y": {
      "field": "Year",
      "type": "ordinal",
      "title": "Năm"
    },
    "x": {
      "field": "Total Collisions",
      "type": "quantitative",
      "title": "Tổng số vụ va chạm"
    },
    "color": {
      "field": "urban_or_rural_area_label",
      "type": "nominal",
      "title": "Khu vực",
      "scale": {
        "domain": ["Urban", "Rural"],
        "range": ["#60A5FA", "#1E40AF"]
      }
    },
    "tooltip": [
      {"field": "Year", "title": "Năm"},
      {"field": "urban_or_rural_area_label", "title": "Khu vực"},
      {"field": "Total Collisions", "title": "Số vụ va chạm", "format": ","}
    ]
  }
}
```

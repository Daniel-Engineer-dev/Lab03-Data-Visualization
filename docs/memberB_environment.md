# HƯỚNG DẪN DENEB: ĐIỀU KIỆN ĐƯỜNG SÁ VÀ MÔI TRƯỜNG (HOÀNG QUỐC VIỆT)

Tài liệu này cung cấp mã JSON Vega-lite để vẽ 4 biểu đồ phân tích về **Điều kiện đường sá và môi trường** dựa trên `dataset_description.md`.
Màu sắc chủ đạo: **Emerald (`#34D399`)**

> **LƯU Ý QUAN TRỌNG:** Phải kéo đúng tên cột từ bảng `Collisions` vào mục **Values** của Deneb visual trước khi dán mã JSON.

---

## 1. Biểu đồ 1: Số vụ va chạm theo loại đường và mức độ (Stacked Bar Chart)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Collisions` > **`road_type_label`**
- `Collisions` > **`collision_severity_label`**
- `Collisions` > **`Total Collisions`** (Measure)

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "mark": {"type": "bar", "cornerRadiusEnd": 2},
  "encoding": {
    "y": {
      "field": "road_type_label",
      "type": "nominal",
      "title": "Loại đường"
    },
    "x": {
      "field": "Total Collisions",
      "type": "quantitative",
      "title": "Tổng số vụ va chạm"
    },
    "color": {
      "field": "collision_severity_label",
      "type": "nominal",
      "title": "Mức độ",
      "scale": {
        "domain": ["Fatal", "Serious", "Slight"],
        "range": ["#EF4444", "#FBBF24", "#34D399"]
      }
    },
    "tooltip": [
      {"field": "road_type_label", "title": "Loại đường"},
      {"field": "collision_severity_label", "title": "Mức độ"},
      {"field": "Total Collisions", "title": "Số vụ va chạm", "format": ","}
    ]
  }
}
```

---

## 2. Biểu đồ 2: Mật độ va chạm theo Thời tiết và Ánh sáng (Heatmap Matrix)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Collisions` > **`weather_conditions_label`**
- `Collisions` > **`light_conditions_label`**
- `Collisions` > **`Total Collisions`** (Measure)

*(Nhớ sử dụng bộ lọc Visual-level filter để loại bỏ các nhãn `Unknown` hoặc `Data missing`)*

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "mark": "rect",
  "encoding": {
    "y": {
      "field": "weather_conditions_label",
      "type": "nominal",
      "title": "Điều kiện thời tiết"
    },
    "x": {
      "field": "light_conditions_label",
      "type": "nominal",
      "title": "Điều kiện ánh sáng",
      "axis": {"labelAngle": -45}
    },
    "color": {
      "field": "Total Collisions",
      "type": "quantitative",
      "title": "Số vụ va chạm",
      "scale": {"scheme": "greens"}
    },
    "tooltip": [
      {"field": "weather_conditions_label", "title": "Thời tiết"},
      {"field": "light_conditions_label", "title": "Ánh sáng"},
      {"field": "Total Collisions", "title": "Số vụ", "format": ","}
    ]
  }
}
```

---

## 3. Biểu đồ 3: Số vụ va chạm theo Giới hạn tốc độ (Bar Chart)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Collisions` > **`speed_limit`**
- `Collisions` > **`Total Collisions`** (Measure)

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "mark": {
    "type": "bar",
    "color": "#34D399",
    "cornerRadiusEnd": 4
  },
  "encoding": {
    "y": {
      "field": "speed_limit",
      "type": "ordinal",
      "title": "Giới hạn tốc độ (mph)",
      "sort": "-y"
    },
    "x": {
      "field": "Total Collisions",
      "type": "quantitative",
      "title": "Tổng số vụ va chạm"
    },
    "tooltip": [
      {"field": "speed_limit", "title": "Tốc độ giới hạn (mph)"},
      {"field": "Total Collisions", "title": "Số vụ", "format": ","}
    ]
  }
}
```

---

## 4. Biểu đồ 4: Số vụ va chạm theo Tình trạng mặt đường & Khu vực (Clustered Column)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Collisions` > **`road_surface_conditions_label`**
- `Collisions` > **`urban_or_rural_area_label`**
- `Collisions` > **`Total Collisions`** (Measure)

*(Lọc bỏ nhãn `Unallocated` và `Unknown` trên Filter pane)*

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "mark": {"type": "bar", "cornerRadiusEnd": 2},
  "encoding": {
    "x": {
      "field": "road_surface_conditions_label",
      "type": "nominal",
      "title": "Tình trạng mặt đường",
      "axis": {"labelAngle": 0}
    },
    "y": {
      "field": "Total Collisions",
      "type": "quantitative",
      "title": "Tổng số vụ va chạm"
    },
    "xOffset": {
      "field": "urban_or_rural_area_label"
    },
    "color": {
      "field": "urban_or_rural_area_label",
      "type": "nominal",
      "title": "Khu vực",
      "scale": {
        "domain": ["Urban", "Rural"],
        "range": ["#34D399", "#059669"]
      }
    },
    "tooltip": [
      {"field": "road_surface_conditions_label", "title": "Mặt đường"},
      {"field": "urban_or_rural_area_label", "title": "Khu vực"},
      {"field": "Total Collisions", "title": "Số vụ", "format": ","}
    ]
  }
}
```

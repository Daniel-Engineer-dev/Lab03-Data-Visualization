# HƯỚNG DẪN DENEB: NGƯỜI THƯƠNG VONG VÀ RỦI RO (PHẠM QUANG VINH)

Tài liệu này cung cấp mã JSON Vega-lite để vẽ 4 biểu đồ phân tích về **Người thương vong và nhóm rủi ro** dựa trên `dataset_description.md`.
Màu sắc chủ đạo: **Red (`#EF4444`)**

> **LƯU Ý QUAN TRỌNG:** Phải kéo đúng tên cột từ bảng `Casualties` vào mục **Values** của Deneb visual trước khi dán mã JSON.

---

## 1. Biểu đồ 1: Thương vong theo nhóm tuổi và mức độ (Stacked Bar Chart)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Casualties` > **`age_band_of_casualty_label`**
- `Casualties` > **`casualty_severity_label`**
- `Casualties` > **`Total Casualties`** (Measure)

*(Loại bỏ các nhãn `Data missing/out of range` bằng Visual Filter)*

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "mark": {"type": "bar", "cornerRadiusEnd": 2},
  "encoding": {
    "y": {
      "field": "age_band_of_casualty_label",
      "type": "ordinal",
      "title": "Nhóm tuổi thương vong"
    },
    "x": {
      "field": "Total Casualties",
      "type": "quantitative",
      "title": "Tổng số thương vong"
    },
    "color": {
      "field": "casualty_severity_label",
      "type": "nominal",
      "title": "Mức độ",
      "scale": {
        "domain": ["Fatal", "Serious", "Slight"],
        "range": ["#EF4444", "#F87171", "#FCA5A5"]
      }
    },
    "tooltip": [
      {"field": "age_band_of_casualty_label", "title": "Nhóm tuổi"},
      {"field": "casualty_severity_label", "title": "Mức độ"},
      {"field": "Total Casualties", "title": "Số lượng", "format": ","}
    ]
  }
}
```

---

## 2. Biểu đồ 2: Thương vong theo vai trò tham gia giao thông (Bar Chart)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Casualties` > **`casualty_class_label`**
- `Casualties` > **`Total Casualties`** (Measure)

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "mark": {
    "type": "bar",
    "color": "#EF4444",
    "cornerRadiusEnd": 4
  },
  "encoding": {
    "y": {
      "field": "casualty_class_label",
      "type": "nominal",
      "title": "Vai trò (Lái xe/Hành khách/Người đi bộ)",
      "sort": "-x"
    },
    "x": {
      "field": "Total Casualties",
      "type": "quantitative",
      "title": "Tổng số thương vong"
    },
    "tooltip": [
      {"field": "casualty_class_label", "title": "Vai trò"},
      {"field": "Total Casualties", "title": "Số lượng", "format": ","}
    ]
  }
}
```

---

## 3. Biểu đồ 3: Thương vong theo nhóm tuổi và giới tính (Clustered Column)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Casualties` > **`age_band_of_casualty_label`**
- `Casualties` > **`sex_of_casualty_label`**
- `Casualties` > **`Total Casualties`** (Measure)

*(Lọc bỏ `Data missing/out of range` và `Unknown`)*

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "mark": {"type": "bar", "cornerRadiusEnd": 2},
  "encoding": {
    "x": {
      "field": "age_band_of_casualty_label",
      "type": "ordinal",
      "title": "Nhóm tuổi",
      "axis": {"labelAngle": -45}
    },
    "y": {
      "field": "Total Casualties",
      "type": "quantitative",
      "title": "Số thương vong"
    },
    "xOffset": {
      "field": "sex_of_casualty_label"
    },
    "color": {
      "field": "sex_of_casualty_label",
      "type": "nominal",
      "title": "Giới tính",
      "scale": {
        "domain": ["Male", "Female", "Unknown/Not provided"],
        "range": ["#EF4444", "#F87171", "#7F1D1D"]
      }
    },
    "tooltip": [
      {"field": "age_band_of_casualty_label", "title": "Nhóm tuổi"},
      {"field": "sex_of_casualty_label", "title": "Giới tính"},
      {"field": "Total Casualties", "title": "Số lượng", "format": ","}
    ]
  }
}
```

---

## 4. Biểu đồ 4: Tỷ lệ mức độ chấn thương theo vai trò (100% Stacked Column)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Casualties` > **`casualty_class_label`**
- `Casualties` > **`casualty_severity_label`**
- `Casualties` > **`Total Casualties`** (Measure)

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "mark": {"type": "bar"},
  "encoding": {
    "x": {
      "field": "casualty_class_label",
      "type": "nominal",
      "title": "Vai trò tham gia giao thông",
      "axis": {"labelAngle": 0}
    },
    "y": {
      "field": "Total Casualties",
      "type": "quantitative",
      "stack": "normalize",
      "title": "Tỷ lệ (%)",
      "axis": {"format": "%"}
    },
    "color": {
      "field": "casualty_severity_label",
      "type": "nominal",
      "title": "Mức độ",
      "scale": {
        "domain": ["Fatal", "Serious", "Slight"],
        "range": ["#EF4444", "#F87171", "#FCA5A5"]
      }
    },
    "tooltip": [
      {"field": "casualty_class_label", "title": "Vai trò"},
      {"field": "casualty_severity_label", "title": "Mức độ"},
      {"field": "Total Casualties", "title": "Thương vong", "format": ","}
    ]
  }
}
```

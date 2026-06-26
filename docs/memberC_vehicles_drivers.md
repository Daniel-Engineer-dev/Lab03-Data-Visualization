# HƯỚNG DẪN DENEB: PHƯƠNG TIỆN VÀ NGƯỜI LÁI (NGUYỄN LÊ THẾ VINH)

Tài liệu này cung cấp mã JSON Vega-lite để vẽ 4 biểu đồ phân tích về **Phương tiện và Người lái** dựa trên `dataset_description.md`.
Màu sắc chủ đạo: **Amber (`#FBBF24`)**

> **LƯU Ý QUAN TRỌNG:** Phải kéo đúng tên cột từ các bảng tương ứng vào mục **Values** của Deneb visual trước khi dán mã JSON.

---

## 1. Biểu đồ 1: Số lượng theo loại phương tiện (Bar Chart)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Vehicles` > **`vehicle_type_label`**
- `Vehicles` > **`Total Vehicles`** (Measure)

*(Nên dùng Filter pane lọc Top 10 phương tiện phổ biến nhất để biểu đồ gọn gàng)*

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "mark": {
    "type": "bar",
    "color": "#FBBF24",
    "cornerRadiusEnd": 4
  },
  "encoding": {
    "y": {
      "field": "vehicle_type_label",
      "type": "nominal",
      "title": "Loại phương tiện",
      "sort": "-x"
    },
    "x": {
      "field": "Total Vehicles",
      "type": "quantitative",
      "title": "Tổng số phương tiện"
    },
    "tooltip": [
      {"field": "vehicle_type_label", "title": "Loại xe"},
      {"field": "Total Vehicles", "title": "Số lượng", "format": ","}
    ]
  }
}
```

---

## 2. Biểu đồ 2: Phương tiện theo nhóm tuổi và giới tính (Stacked Column Chart)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Vehicles` > **`age_band_of_driver_label`**
- `Vehicles` > **`sex_of_driver_label`**
- `Vehicles` > **`Total Vehicles`** (Measure)

*(Lọc bỏ các nhãn `Data missing/out of range` hoặc `Unknown`)*

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "mark": {"type": "bar", "cornerRadiusEnd": 2},
  "encoding": {
    "x": {
      "field": "age_band_of_driver_label",
      "type": "ordinal",
      "title": "Nhóm tuổi người lái",
      "axis": {"labelAngle": -45}
    },
    "y": {
      "field": "Total Vehicles",
      "type": "quantitative",
      "title": "Tổng số phương tiện"
    },
    "color": {
      "field": "sex_of_driver_label",
      "type": "nominal",
      "title": "Giới tính",
      "scale": {
        "domain": ["Male", "Female", "Unknown/Not provided"],
        "range": ["#FBBF24", "#F59E0B", "#B45309"]
      }
    },
    "tooltip": [
      {"field": "age_band_of_driver_label", "title": "Nhóm tuổi"},
      {"field": "sex_of_driver_label", "title": "Giới tính"},
      {"field": "Total Vehicles", "title": "Số lượng", "format": ","}
    ]
  }
}
```

---

## 3. Biểu đồ 3: Tỷ lệ phương tiện tham gia va chạm theo khu vực (Donut Chart)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Collisions` > **`urban_or_rural_area_label`**
- `Vehicles` > **`Total Vehicles`** (Measure)

*(Loại bỏ nhãn `Unallocated`)*

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "mark": {"type": "arc", "innerRadius": 50},
  "encoding": {
    "theta": {"field": "Total Vehicles", "type": "quantitative"},
    "color": {
      "field": "urban_or_rural_area_label",
      "type": "nominal",
      "title": "Khu vực",
      "scale": {
        "domain": ["Urban", "Rural"],
        "range": ["#FBBF24", "#D97706"]
      }
    },
    "tooltip": [
      {"field": "urban_or_rural_area_label", "title": "Khu vực"},
      {"field": "Total Vehicles", "title": "Số lượng", "format": ","}
    ]
  }
}
```

---

## 4. Biểu đồ 4: Số phương tiện và tỷ lệ tai nạn nặng theo nhóm tuổi (Dual Axis Line/Column Chart)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Vehicles` > **`age_band_of_driver_label`**
- `Vehicles` > **`Total Vehicles`** (Measure)
- `Collisions` > **`Serious Casualties`** (Measure, được dùng đại diện cho mức độ nặng)

*(Loại bỏ `Data missing/out of range`)*

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "resolve": {"scale": {"y": "independent"}},
  "layer": [
    {
      "mark": {"type": "bar", "color": "#FBBF24"},
      "encoding": {
        "x": {
          "field": "age_band_of_driver_label",
          "type": "ordinal",
          "title": "Nhóm tuổi",
          "axis": {"labelAngle": -45}
        },
        "y": {
          "field": "Total Vehicles",
          "type": "quantitative",
          "title": "Số lượng phương tiện"
        },
        "tooltip": [
          {"field": "age_band_of_driver_label", "title": "Nhóm tuổi"},
          {"field": "Total Vehicles", "title": "Tổng phương tiện", "format": ","}
        ]
      }
    },
    {
      "mark": {"type": "line", "color": "#EF4444", "strokeWidth": 3, "point": true},
      "encoding": {
        "x": {
          "field": "age_band_of_driver_label",
          "type": "ordinal"
        },
        "y": {
          "field": "Serious Casualties",
          "type": "quantitative",
          "title": "Số ca thương vong nặng (Serious)"
        },
        "tooltip": [
          {"field": "age_band_of_driver_label", "title": "Nhóm tuổi"},
          {"field": "Serious Casualties", "title": "Thương vong nặng", "format": ","}
        ]
      }
    }
  ]
}
```

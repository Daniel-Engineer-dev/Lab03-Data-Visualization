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
  "config": {
    "font": "system-ui, -apple-system, sans-serif",
    "view": {"stroke": "transparent"},
    "axis": {
      "domainColor": "#E5E7EB",
      "tickColor": "#E5E7EB",
      "labelColor": "#6B7280",
      "labelFontSize": 12,
      "titleColor": "#4B5563",
      "titleFontWeight": 600,
      "titlePadding": 12
    }
  },
  "title": {
    "text": "Số lượng theo loại phương tiện (Top 10)",
    "anchor": "start",
    "fontSize": 18,
    "fontWeight": 700,
    "color": "#111827",
    "offset": 20
  },
  "data": {"name": "dataset"},
  "transform": [
    {
      "filter": "datum.vehicle_type_label != 'Data missing or out of range' && datum.vehicle_type_label != 'Unknown'"
    },
    {
      "window": [{"op": "rank", "as": "rank"}],
      "sort": [{"field": "Total Vehicles", "order": "descending"}]
    },
    {
      "filter": "datum.rank <= 10"
    }
  ],
  "encoding": {
    "y": {
      "field": "vehicle_type_label",
      "type": "nominal",
      "title": null,
      "sort": "-x",
      "axis": {"labelLimit": 150}
    },
    "x": {
      "field": "Total Vehicles",
      "type": "quantitative",
      "title": null,
      "axis": {"grid": false, "labels": false, "ticks": false, "domain": false}
    }
  },
  "layer": [
    {
      "params": [
        {
          "name": "hover",
          "select": {"type": "point", "on": "pointerover"}
        }
      ],
      "mark": {
        "type": "bar",
        "cornerRadiusEnd": 6
      },
      "encoding": {
        "color": {
          "condition": {"test": "datum.rank == 1", "value": "#10B981"},
          "value": "#D1FAE5"
        },
        "opacity": {
          "condition": {"param": "hover", "value": 1},
          "value": 0.7
        },
        "tooltip": [
          {"field": "vehicle_type_label", "title": "Loại xe"},
          {"field": "Total Vehicles", "title": "Số lượng", "format": ","}
        ]
      }
    },
    {
      "mark": {
        "type": "text",
        "align": "left",
        "dx": 8,
        "fontSize": 12,
        "fontWeight": 600,
        "color": "#374151"
      },
      "encoding": {
        "text": {
          "field": "Total Vehicles",
          "type": "quantitative",
          "format": ","
        }
      }
    }
  ]
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
  "config": {
    "font": "system-ui, -apple-system, sans-serif",
    "view": {"stroke": "transparent"},
    "axis": {
      "domainColor": "#E5E7EB",
      "tickColor": "#E5E7EB",
      "labelColor": "#6B7280",
      "labelFontSize": 12,
      "titleColor": "#4B5563",
      "titleFontWeight": 600,
      "titlePadding": 12
    },
    "legend": {"titleColor": "#4B5563", "labelColor": "#6B7280", "orient": "top-right"}
  },
  "title": {
    "text": "Phương tiện theo nhóm tuổi và giới tính",
    "anchor": "start",
    "fontSize": 18,
    "fontWeight": 700,
    "color": "#111827",
    "offset": 20
  },
  "data": {"name": "dataset"},
  "transform": [
    {
      "filter": "datum.age_band_of_driver_label != 'Data missing or out of range' && datum.age_band_of_driver_label != 'Unknown'"
    },
    {
      "calculate": "datum.sex_of_driver_label == 'Male' ? 'Nam' : datum.sex_of_driver_label == 'Female' ? 'Nữ' : 'Không xác định'",
      "as": "GioiTinh_VN"
    }
  ],
  "params": [
    {
      "name": "hover",
      "select": {"type": "point", "on": "pointerover", "fields": ["GioiTinh_VN"]}
    }
  ],
  "mark": {"type": "bar", "cornerRadiusTopLeft": 6, "cornerRadiusTopRight": 6},
  "encoding": {
    "opacity": {
      "condition": {"param": "hover", "value": 1},
      "value": 0.7
    },
    "x": {
      "field": "age_band_of_driver_label",
      "type": "ordinal",
      "title": "Nhóm tuổi người lái",
      "sort": ["0 - 5", "6 - 10", "11 - 15", "16 - 20", "21 - 25", "26 - 35", "36 - 45", "46 - 55", "56 - 65", "66 - 75", "Over 75"],
      "axis": {"labelAngle": -45}
    },
    "y": {
      "field": "Total Vehicles",
      "type": "quantitative",
      "title": "Tổng số phương tiện"
    },
    "color": {
      "field": "GioiTinh_VN",
      "type": "nominal",
      "title": "Giới tính",
      "scale": {
        "domain": ["Nam", "Nữ", "Không xác định"],
        "range": ["#2563EB", "#EC4899", "#E5E7EB"]
      }
    },
    "tooltip": [
      {"field": "age_band_of_driver_label", "title": "Nhóm tuổi"},
      {"field": "GioiTinh_VN", "title": "Giới tính"},
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
  "config": {
    "font": "system-ui, -apple-system, sans-serif",
    "view": {"stroke": "transparent"},
    "legend": {"titleColor": "#4B5563", "labelColor": "#6B7280", "orient": "top-right"}
  },
  "title": {
    "text": "Tỷ lệ phương tiện tham gia va chạm theo khu vực",
    "anchor": "start",
    "fontSize": 18,
    "fontWeight": 700,
    "color": "#111827",
    "offset": 20
  },
  "data": {"name": "dataset"},
  "transform": [
    {
      "filter": "datum.urban_or_rural_area_label != 'Unallocated' && datum.urban_or_rural_area_label != 'Unknown' && isValid(datum['Total Vehicles']) && datum['Total Vehicles'] > 0"
    },
    {
      "calculate": "datum.urban_or_rural_area_label == 'Urban' ? 'Thành thị' : datum.urban_or_rural_area_label == 'Rural' ? 'Nông thôn' : datum.urban_or_rural_area_label",
      "as": "KhuVuc_VN"
    },
    {
      "joinaggregate": [{"op": "sum", "field": "Total Vehicles", "as": "GrandTotal"}]
    },
    {
      "calculate": "datum['Total Vehicles'] / datum.GrandTotal",
      "as": "Percent"
    }
  ],
  "encoding": {
    "theta": {"field": "Total Vehicles", "type": "quantitative"},
    "color": {
      "field": "KhuVuc_VN",
      "type": "nominal",
      "title": "Khu vực",
      "scale": {
        "domain": ["Thành thị", "Nông thôn"],
        "range": ["#6366F1", "#F59E0B"]
      }
    }
  },
  "layer": [
    {
      "params": [
        {
          "name": "hover",
          "select": {"type": "point", "on": "pointerover"}
        }
      ],
      "mark": {"type": "arc", "innerRadius": 50, "outerRadius": 100, "stroke": "#FFFFFF", "strokeWidth": 2},
      "encoding": {
        "opacity": {
          "condition": {"param": "hover", "value": 1},
          "value": 0.8
        },
        "tooltip": [
          {"field": "KhuVuc_VN", "title": "Khu vực"},
          {"field": "Total Vehicles", "title": "Số lượng", "format": ","},
          {"field": "Percent", "title": "Tỷ lệ", "format": ".1%"}
        ]
      }
    },
    {
      "mark": {"type": "text", "fontWeight": 700, "fontSize": 14, "radius": 75},
      "encoding": {
        "theta": {"field": "Total Vehicles", "type": "quantitative", "stack": true},
        "detail": {"field": "KhuVuc_VN", "type": "nominal"},
        "text": {"field": "Percent", "type": "quantitative", "format": ".1%"},
        "color": {"value": "#1F2937"},
        "opacity": {
          "condition": {"test": "datum.Percent > 0.001", "value": 1},
          "value": 0
        }
      }
    }
  ]
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
  "config": {
    "font": "system-ui, -apple-system, sans-serif",
    "view": {"stroke": "transparent"},
    "axis": {
      "domainColor": "#E5E7EB",
      "tickColor": "#E5E7EB",
      "labelColor": "#6B7280",
      "labelFontSize": 12,
      "titleColor": "#4B5563",
      "titleFontWeight": 600,
      "titlePadding": 12
    }
  },
  "title": {
    "text": "Phương tiện và thương vong nặng theo nhóm tuổi",
    "anchor": "start",
    "fontSize": 18,
    "fontWeight": 700,
    "color": "#111827",
    "offset": 20
  },
  "data": {"name": "dataset"},
  "transform": [
    {
      "filter": "datum.age_band_of_driver_label != 'Data missing or out of range' && datum.age_band_of_driver_label != 'Unknown'"
    }
  ],
  "resolve": {"scale": {"y": "independent"}},
  "layer": [
    {
      "params": [
        {
          "name": "hover",
          "select": {"type": "point", "on": "pointerover"}
        }
      ],
      "mark": {"type": "bar", "color": "#DBEAFE", "cornerRadiusTopLeft": 6, "cornerRadiusTopRight": 6},
      "encoding": {
        "opacity": {
          "condition": {"param": "hover", "value": 1},
          "value": 0.7
        },
        "x": {
          "field": "age_band_of_driver_label",
          "type": "ordinal",
          "title": "Nhóm tuổi",
          "sort": ["0 - 5", "6 - 10", "11 - 15", "16 - 20", "21 - 25", "26 - 35", "36 - 45", "46 - 55", "56 - 65", "66 - 75", "Over 75"],
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
      "mark": {"type": "line", "color": "#9333EA", "strokeWidth": 3, "interpolate": "monotone", "point": {"filled": true, "fill": "#FFFFFF", "stroke": "#9333EA", "strokeWidth": 2, "size": 60}},
      "encoding": {
        "x": {
          "field": "age_band_of_driver_label",
          "type": "ordinal",
          "sort": ["0 - 5", "6 - 10", "11 - 15", "16 - 20", "21 - 25", "26 - 35", "36 - 45", "46 - 55", "56 - 65", "66 - 75", "Over 75"]
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

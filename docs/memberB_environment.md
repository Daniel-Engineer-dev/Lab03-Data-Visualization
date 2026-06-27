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
  "title": {
    "text": "Số vụ va chạm theo loại đường và mức độ",
    "anchor": "start",
    "fontSize": 16,
    "offset": 10
  },
  "data": {
    "name": "dataset"
  },
  "transform": [
    {
      "calculate": "datum.road_type_label == 'Dual carriageway' ? 'Đường đôi' : datum.road_type_label == 'One way street' ? 'Đường 1 chiều' : datum.road_type_label == 'Roundabout' ? 'Vòng xuyến' : datum.road_type_label == 'Single carriageway' ? 'Đường đơn' : datum.road_type_label == 'Slip road' ? 'Đường nhánh' : 'Không rõ'",
      "as": "LoaiDuong_VN"
    },
    {
      "calculate": "datum.collision_severity_label == 'Fatal' ? 'Tử vong' : datum.collision_severity_label == 'Serious' ? 'Nghiêm trọng' : 'Nhẹ'",
      "as": "MucDo_VN"
    }
  ],
  "params": [
    {
      "name": "hover",
      "select": {
        "type": "point",
        "on": "pointerover"
      }
    },
    {
      "name": "click",
      "select": {
        "type": "point"
      }
    }
  ],
  "mark": {
    "type": "bar",
    "cornerRadiusEnd": 2
  },
  "encoding": {
    "opacity": {
      "condition": {
        "param": "click",
        "value": 1
      },
      "value": 0.3
    },
    "x": {
      "field": "LoaiDuong_VN",
      "type": "nominal",
      "title": "Loại đường",
      "axis": {
        "labelAngle": -45
      }
    },
    "y": {
      "field": "Total Collisions",
      "type": "quantitative",
      "title": "Tổng số vụ va chạm"
    },
    "color": {
      "field": "MucDo_VN",
      "type": "nominal",
      "title": "Mức độ",
      "scale": {
        "domain": [
          "Tử vong",
          "Nghiêm trọng",
          "Nhẹ"
        ],
        "range": [
          "#EF4444",
          "#FBBF24",
          "#34D399"
        ]
      }
    },
    "tooltip": [
      {
        "field": "LoaiDuong_VN",
        "title": "Loại đường"
      },
      {
        "field": "MucDo_VN",
        "title": "Mức độ"
      },
      {
        "field": "Total Collisions",
        "title": "Số vụ va chạm",
        "format": ","
      }
    ]
  },
  "config": {
    "font": "Segoe UI"
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
  "title": {
    "text": "Mật độ va chạm theo Thời tiết và Ánh sáng",
    "anchor": "start",
    "fontSize": 16,
    "offset": 10
  },
  "data": {
    "name": "dataset"
  },
  "transform": [
    {
      "calculate": "datum.weather_conditions_label == 'Fine no high winds' ? 'Nắng (không gió)' : datum.weather_conditions_label == 'Raining no high winds' ? 'Mưa (không gió)' : datum.weather_conditions_label == 'Snowing no high winds' ? 'Tuyết (không gió)' : datum.weather_conditions_label == 'Fine + high winds' ? 'Nắng + Gió lớn' : datum.weather_conditions_label == 'Raining + high winds' ? 'Mưa + Gió lớn' : datum.weather_conditions_label == 'Snowing + high winds' ? 'Tuyết + Gió lớn' : datum.weather_conditions_label == 'Fog or mist' ? 'Sương mù' : datum.weather_conditions_label == 'Other' ? 'Khác' : 'Không rõ'",
      "as": "ThoiTiet_VN"
    },
    {
      "calculate": "datum.light_conditions_label == 'Daylight' ? 'Ban ngày' : datum.light_conditions_label == 'Darkness - lights lit' ? 'Tối (có đèn)' : datum.light_conditions_label == 'Darkness - lights unlit' ? 'Tối (đèn tắt)' : datum.light_conditions_label == 'Darkness - no lighting' ? 'Tối (không đèn)' : 'Tối (không rõ đèn)'",
      "as": "AnhSang_VN"
    }
  ],
  "params": [
    {
      "name": "hover",
      "select": {
        "type": "point",
        "on": "pointerover"
      }
    },
    {
      "name": "click",
      "select": {
        "type": "point"
      }
    }
  ],
  "mark": "rect",
  "encoding": {
    "opacity": {
      "condition": {
        "param": "click",
        "value": 1
      },
      "value": 0.3
    },
    "y": {
      "field": "ThoiTiet_VN",
      "type": "nominal",
      "title": "Điều kiện thời tiết"
    },
    "x": {
      "field": "AnhSang_VN",
      "type": "nominal",
      "title": "Điều kiện ánh sáng",
      "axis": {
        "labelAngle": -45
      }
    },
    "color": {
      "field": "Total Collisions",
      "type": "quantitative",
      "title": "Số vụ va chạm",
      "scale": {
        "type": "sqrt",
        "scheme": "greens"
      }
    },
    "tooltip": [
      {
        "field": "ThoiTiet_VN",
        "title": "Thời tiết"
      },
      {
        "field": "AnhSang_VN",
        "title": "Ánh sáng"
      },
      {
        "field": "Total Collisions",
        "title": "Số vụ",
        "format": ","
      }
    ]
  },
  "config": {
    "font": "Segoe UI"
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
  "title": {
    "text": "Số vụ va chạm theo giới hạn tốc độ",
    "anchor": "start",
    "fontSize": 16,
    "offset": 10
  },
  "data": {
    "name": "dataset"
  },
  "transform": [
    {
      "calculate": "datum.speed_limit == -1 || datum.speed_limit == 'Unknown' ? 'Không rõ' : datum.speed_limit",
      "as": "TocDo_VN"
    }
  ],
  "params": [
    {
      "name": "hover",
      "select": {
        "type": "point",
        "on": "pointerover"
      }
    },
    {
      "name": "click",
      "select": {
        "type": "point"
      }
    }
  ],
  "mark": {
    "type": "bar",
    "color": "#34D399",
    "cornerRadiusEnd": 4
  },
  "encoding": {
    "opacity": {
      "condition": {
        "param": "click",
        "value": 1
      },
      "value": 0.3
    },
    "x": {
      "field": "TocDo_VN",
      "type": "ordinal",
      "title": "Giới hạn tốc độ (mph)",
      "axis": {
        "labelAngle": 0
      }
    },
    "y": {
      "field": "Total Collisions",
      "type": "quantitative",
      "title": "Tổng số vụ va chạm"
    },
    "tooltip": [
      {
        "field": "TocDo_VN",
        "title": "Tốc độ giới hạn (mph)"
      },
      {
        "field": "Total Collisions",
        "title": "Số vụ",
        "format": ","
      }
    ]
  },
  "config": {
    "font": "Segoe UI"
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
  "title": {
    "text": "Số vụ va chạm theo Tình trạng mặt đường & Khu vực",
    "anchor": "start",
    "fontSize": 16,
    "offset": 10
  },
  "data": {
    "name": "dataset"
  },
  "transform": [
    {
      "calculate": "datum.road_surface_conditions_label == 'Dry' ? 'Khô ráo' : datum.road_surface_conditions_label == 'Wet or damp' ? 'Ẩm ướt' : datum.road_surface_conditions_label == 'Snow' ? 'Tuyết' : datum.road_surface_conditions_label == 'Frost or ice' ? 'Băng giá' : datum.road_surface_conditions_label == 'Flood over 3cm. deep' ? 'Ngập lụt' : datum.road_surface_conditions_label == 'Oil or diesel' ? 'Dầu mỡ' : datum.road_surface_conditions_label == 'Mud' ? 'Bùn đất' : 'Khác'",
      "as": "MatDuong_VN"
    },
    {
      "calculate": "datum.urban_or_rural_area_label == 'Urban' ? 'Thành thị' : datum.urban_or_rural_area_label == 'Rural' ? 'Nông thôn' : 'Khác'",
      "as": "KhuVuc_VN"
    }
  ],
  "params": [
    {
      "name": "hover",
      "select": {
        "type": "point",
        "on": "pointerover"
      }
    },
    {
      "name": "click",
      "select": {
        "type": "point"
      }
    }
  ],
  "mark": {
    "type": "bar",
    "cornerRadiusEnd": 2
  },
  "encoding": {
    "opacity": {
      "condition": {
        "param": "click",
        "value": 1
      },
      "value": 0.3
    },
    "x": {
      "field": "MatDuong_VN",
      "type": "nominal",
      "title": "Tình trạng mặt đường",
      "axis": {
        "labelAngle": 0
      }
    },
    "y": {
      "field": "Total Collisions",
      "type": "quantitative",
      "title": "Tổng số vụ va chạm"
    },
    "xOffset": {
      "field": "KhuVuc_VN"
    },
    "color": {
      "field": "KhuVuc_VN",
      "type": "nominal",
      "title": "Khu vực",
      "scale": {
        "domain": [
          "Thành thị",
          "Nông thôn"
        ],
        "range": [
          "#34D399",
          "#059669"
        ]
      }
    },
    "tooltip": [
      {
        "field": "MatDuong_VN",
        "title": "Mặt đường"
      },
      {
        "field": "KhuVuc_VN",
        "title": "Khu vực"
      },
      {
        "field": "Total Collisions",
        "title": "Số vụ",
        "format": ","
      }
    ]
  },
  "config": {
    "font": "Segoe UI"
  }
}
```

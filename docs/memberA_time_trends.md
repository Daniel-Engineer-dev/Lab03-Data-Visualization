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
  "config": {
    "font": "Segoe UI"
  },
  "title": {
    "text": "Số vụ va chạm theo năm và mức độ",
    "anchor": "start",
    "fontSize": 16,
    "offset": 10
  },
  "data": {
    "name": "dataset"
  },
  "transform": [
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
        "on": "pointerover",
        "fields": [
          "MucDo_VN"
        ]
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
    "type": "line",
    "strokeWidth": 3,
    "point": {
      "filled": true
    }
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
      "field": "Year",
      "type": "ordinal",
      "title": "Năm",
      "axis": {
        "labelAngle": 0
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
      "title": "Mức độ nghiêm trọng",
      "scale": {
        "domain": [
          "Tử vong",
          "Nghiêm trọng",
          "Nhẹ"
        ],
        "range": [
          "#EF4444",
          "#FBBF24",
          "#60A5FA"
        ]
      }
    },
    "tooltip": [
      {
        "field": "Year",
        "title": "Năm"
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
  "title": {
    "text": "Số vụ va chạm theo tháng",
    "anchor": "start",
    "fontSize": 16,
    "offset": 10
  },
  "data": {
    "name": "dataset"
  },
  "transform": [
    {
      "calculate": "'Tháng ' + datum['Month Number']",
      "as": "Thang_VN"
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
    "color": "#60A5FA",
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
      "field": "Thang_VN",
      "type": "nominal",
      "title": "Tháng",
      "sort": {
        "field": "Month Number"
      },
      "axis": {
        "labelAngle": -45
      }
    },
    "y": {
      "field": "Total Collisions",
      "type": "quantitative",
      "title": "Tổng số vụ va chạm"
    },
    "tooltip": [
      {
        "field": "Thang_VN",
        "title": "Tháng"
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

## 3. Biểu đồ 3: Mật độ va chạm theo Thứ và Giờ (Heatmap Matrix)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Collisions` > **`day_of_week_label`**
- `Collisions` > **`time`** (Sẽ trích xuất theo giờ)
- `Collisions` > **`Total Collisions`** (Measure)

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "title": {
    "text": "Mật độ va chạm theo Thứ và Giờ",
    "anchor": "start",
    "fontSize": 16,
    "offset": 10
  },
  "data": {
    "name": "dataset"
  },
  "transform": [
    {
      "calculate": "datum.day_of_week_label == 'Monday' ? 'Thứ 2' : datum.day_of_week_label == 'Tuesday' ? 'Thứ 3' : datum.day_of_week_label == 'Wednesday' ? 'Thứ 4' : datum.day_of_week_label == 'Thursday' ? 'Thứ 5' : datum.day_of_week_label == 'Friday' ? 'Thứ 6' : datum.day_of_week_label == 'Saturday' ? 'Thứ 7' : 'Chủ nhật'",
      "as": "Thu_VN"
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
      "field": "Thu_VN",
      "type": "nominal",
      "title": "Thứ trong tuần",
      "sort": [
        "Thứ 2",
        "Thứ 3",
        "Thứ 4",
        "Thứ 5",
        "Thứ 6",
        "Thứ 7",
        "Chủ nhật"
      ]
    },
    "x": {
      "field": "time",
      "type": "ordinal",
      "timeUnit": "hours",
      "title": "Giờ trong ngày",
      "axis": {
        "format": "%H:00",
        "labelAngle": -45
      }
    },
    "color": {
      "aggregate": "sum",
      "field": "Total Collisions",
      "type": "quantitative",
      "title": "Số vụ va chạm",
      "scale": {
        "scheme": "blues"
      }
    },
    "tooltip": [
      {
        "field": "Thu_VN",
        "title": "Thứ"
      },
      {
        "field": "time",
        "timeUnit": "hours",
        "title": "Giờ",
        "format": "%H:00"
      },
      {
        "aggregate": "sum",
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

## 4. Biểu đồ 4: Số vụ va chạm theo năm và khu vực (Stacked Bar Chart)
**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Calendar` > **`Year`**
- `Collisions` > **`urban_or_rural_area_label`**
- `Collisions` > **`Total Collisions`** (Measure)

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**
```json
{
  "title": {
    "text": "Số vụ va chạm theo năm và khu vực",
    "anchor": "start",
    "fontSize": 16,
    "offset": 10
  },
  "data": {
    "name": "dataset"
  },
  "transform": [
    {
      "calculate": "datum.urban_or_rural_area_label == 'Urban' ? 'Thành thị' : datum.urban_or_rural_area_label == 'Rural' ? 'Nông thôn' : datum.urban_or_rural_area_label",
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
      "field": "KhuVuc_VN",
      "type": "nominal",
      "title": "Khu vực",
      "scale": {
        "domain": [
          "Thành thị",
          "Nông thôn"
        ],
        "range": [
          "#60A5FA",
          "#1E40AF"
        ]
      }
    },
    "tooltip": [
      {
        "field": "Year",
        "title": "Năm"
      },
      {
        "field": "KhuVuc_VN",
        "title": "Khu vực"
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

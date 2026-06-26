# HƯỚNG DẪN DENEB: NGƯỜI THƯƠNG VONG VÀ NHÓM RỦI RO (PHẠM QUANG VINH)

Tài liệu này cung cấp mã JSON Vega-Lite để vẽ các biểu đồ phân tích về **người thương vong và nhóm rủi ro** dựa trên `dataset_description.md`.

Các biểu đồ dưới đây đã được chỉnh để:

- Hiển thị nhãn tiếng Việt trên tiêu đề, trục, chú giải và tooltip.
- Sort nhóm tuổi theo thứ tự tự nhiên thay vì theo chữ.
- Sort mức độ thương vong theo thứ tự rủi ro: **Tử vong → Nghiêm trọng → Nhẹ**.
- Dùng màu phân biệt nhóm, không để toàn bộ biểu đồ chỉ có một màu.
- Lọc các nhóm thiếu dữ liệu ngay trong Vega-Lite spec khi biểu đồ cần so sánh nhóm thật.

> **LƯU Ý QUAN TRỌNG:** Phải kéo đúng tên cột từ bảng `Casualties` vào mục **Values** của Deneb visual trước khi dán mã JSON.

---

## Quy ước màu và thứ tự

### Mức độ thương vong

| Label gốc | Label hiển thị | Màu | Ý nghĩa |
|---|---|---|---|
| `Fatal` | `Tử vong` | `#DC2626` | Mức nặng nhất |
| `Serious` | `Nghiêm trọng` | `#F97316` | Bị thương nặng |
| `Slight` | `Nhẹ` | `#60A5FA` | Bị thương nhẹ |

### Vai trò tham gia giao thông

| Label gốc | Label hiển thị | Màu |
|---|---|---|
| `Driver or rider` | `Người điều khiển` | `#2563EB` |
| `Passenger` | `Hành khách` | `#14B8A6` |
| `Pedestrian` | `Người đi bộ` | `#F59E0B` |

---

## 1. Biểu đồ 1: Thương vong theo nhóm tuổi và mức độ

**Mục tiêu:** Xác định nhóm tuổi có số người thương vong cao và xem mức độ `Tử vong`, `Nghiêm trọng`, `Nhẹ` phân bố như thế nào trong từng nhóm tuổi.

**Loại biểu đồ:** Stacked Bar Chart.

**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**

- `Casualties` > **`age_band_of_casualty_label`**
- `Casualties` > **`casualty_severity_label`**
- `Casualties` > **`Total Casualties`** (Measure)

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**

```json
{
  "data": {"name": "dataset"},
  "title": {
    "text": "Số người thương vong theo nhóm tuổi và mức độ",
    "anchor": "middle",
    "fontSize": 15,
    "fontWeight": "bold",
    "dy": -5
  },
  "transform": [
    {
      "filter": "datum.age_band_of_casualty_label != 'Data missing or out of range' && datum.age_band_of_casualty_label != null"
    },
    {
      "calculate": "datum.casualty_severity_label == 'Fatal' ? 'Tử vong' : datum.casualty_severity_label == 'Serious' ? 'Nghiêm trọng' : datum.casualty_severity_label == 'Slight' ? 'Nhẹ' : datum.casualty_severity_label",
      "as": "Mức độ thương vong"
    },
    {
      "calculate": "datum.casualty_severity_label == 'Fatal' ? 1 : datum.casualty_severity_label == 'Serious' ? 2 : datum.casualty_severity_label == 'Slight' ? 3 : 99",
      "as": "severity_order"
    },
    {
      "calculate": "datum.age_band_of_casualty_label == '0 - 5' ? 1 : datum.age_band_of_casualty_label == '6 - 10' ? 2 : datum.age_band_of_casualty_label == '11 - 15' ? 3 : datum.age_band_of_casualty_label == '16 - 20' ? 4 : datum.age_band_of_casualty_label == '21 - 25' ? 5 : datum.age_band_of_casualty_label == '26 - 35' ? 6 : datum.age_band_of_casualty_label == '36 - 45' ? 7 : datum.age_band_of_casualty_label == '46 - 55' ? 8 : datum.age_band_of_casualty_label == '56 - 65' ? 9 : datum.age_band_of_casualty_label == '66 - 75' ? 10 : datum.age_band_of_casualty_label == 'Over 75' ? 11 : 99",
      "as": "age_order"
    }
  ],
  "mark": {"type": "bar", "cornerRadiusEnd": 2},
  "encoding": {
    "y": {
      "field": "age_band_of_casualty_label",
      "type": "ordinal",
      "title": "Nhóm tuổi",
      "sort": {"field": "age_order", "order": "descending"}
    },
    "x": {
      "field": "Total Casualties",
      "type": "quantitative",
      "title": "Số người thương vong",
      "axis": {"format": "~s"}
    },
    "color": {
      "field": "Mức độ thương vong",
      "type": "nominal",
      "title": "Mức độ thương vong",
      "scale": {
        "domain": ["Tử vong", "Nghiêm trọng", "Nhẹ"],
        "range": ["#DC2626", "#F97316", "#60A5FA"]
      },
      "legend": {"orient": "top", "direction": "horizontal"}
    },
    "order": {
      "field": "severity_order",
      "type": "quantitative",
      "sort": "ascending"
    },
    "tooltip": [
      {"field": "age_band_of_casualty_label", "title": "Nhóm tuổi"},
      {"field": "Mức độ thương vong", "title": "Mức độ"},
      {"field": "Total Casualties", "title": "Số người thương vong", "format": ","}
    ]
  }
}
```

**Gợi ý đọc biểu đồ:** Nếu muốn tuổi nhỏ ở trên và tuổi lớn ở dưới, đổi `"order": "descending"` trong phần `y.sort` thành `"ascending"`.

---

## 2. Biểu đồ 2: Thương vong theo vai trò tham gia giao thông

**Mục tiêu:** So sánh tổng số người thương vong giữa các vai trò tham gia giao thông.

**Loại biểu đồ:** Bar Chart.

**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**

- `Casualties` > **`casualty_class_label`**
- `Casualties` > **`Total Casualties`** (Measure)

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**

```json
{
  "data": {"name": "dataset"},
  "title": {
    "text": "Số người thương vong theo vai trò tham gia giao thông",
    "anchor": "middle",
    "fontSize": 15,
    "fontWeight": "bold",
    "dy": -5
  },
  "transform": [
    {
      "calculate": "datum.casualty_class_label == 'Driver or rider' ? 'Người điều khiển' : datum.casualty_class_label == 'Passenger' ? 'Hành khách' : datum.casualty_class_label == 'Pedestrian' ? 'Người đi bộ' : datum.casualty_class_label",
      "as": "Vai trò"
    },
    {
      "calculate": "datum.casualty_class_label == 'Driver or rider' ? 1 : datum.casualty_class_label == 'Passenger' ? 2 : datum.casualty_class_label == 'Pedestrian' ? 3 : 99",
      "as": "role_order"
    }
  ],
  "mark": {
    "type": "bar",
    "cornerRadiusEnd": 4
  },
  "encoding": {
    "y": {
      "field": "Vai trò",
      "type": "nominal",
      "title": "Vai trò tham gia giao thông",
      "sort": {"field": "Total Casualties", "order": "descending"}
    },
    "x": {
      "field": "Total Casualties",
      "type": "quantitative",
      "title": "Số người thương vong",
      "axis": {"format": "~s"}
    },
    "color": {
      "field": "Vai trò",
      "type": "nominal",
      "title": "Vai trò",
      "scale": {
        "domain": ["Người điều khiển", "Hành khách", "Người đi bộ"],
        "range": ["#2563EB", "#14B8A6", "#F59E0B"]
      },
      "legend": null
    },
    "tooltip": [
      {"field": "Vai trò", "title": "Vai trò"},
      {"field": "Total Casualties", "title": "Số người thương vong", "format": ","}
    ]
  }
}
```

**Gợi ý đọc biểu đồ:** Biểu đồ này nên sort giảm dần theo số người thương vong để người xem nhận ra ngay nhóm có quy mô lớn nhất.

---

## 3. Biểu đồ 3: Thương vong theo nhóm tuổi và giới tính

**Mục tiêu:** So sánh số người thương vong theo giới tính trong từng nhóm tuổi.

**Loại biểu đồ:** Clustered Column Chart.

**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**

- `Casualties` > **`age_band_of_casualty_label`**
- `Casualties` > **`sex_of_casualty_label`**
- `Casualties` > **`Total Casualties`** (Measure)

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**

```json
{
  "data": {"name": "dataset"},
  "title": {
    "text": "Số người thương vong theo nhóm tuổi và giới tính",
    "anchor": "middle",
    "fontSize": 15,
    "fontWeight": "bold",
    "dy": -5
  },
  "transform": [
    {
      "filter": "datum.age_band_of_casualty_label != 'Data missing or out of range' && datum.age_band_of_casualty_label != null && datum.sex_of_casualty_label != 'Data missing or out of range' && datum.sex_of_casualty_label != 'unknown (self reported)' && datum.sex_of_casualty_label != null"
    },
    {
      "calculate": "datum.sex_of_casualty_label == 'Male' ? 'Nam' : datum.sex_of_casualty_label == 'Female' ? 'Nữ' : datum.sex_of_casualty_label",
      "as": "Giới tính"
    },
    {
      "calculate": "datum.age_band_of_casualty_label == '0 - 5' ? 1 : datum.age_band_of_casualty_label == '6 - 10' ? 2 : datum.age_band_of_casualty_label == '11 - 15' ? 3 : datum.age_band_of_casualty_label == '16 - 20' ? 4 : datum.age_band_of_casualty_label == '21 - 25' ? 5 : datum.age_band_of_casualty_label == '26 - 35' ? 6 : datum.age_band_of_casualty_label == '36 - 45' ? 7 : datum.age_band_of_casualty_label == '46 - 55' ? 8 : datum.age_band_of_casualty_label == '56 - 65' ? 9 : datum.age_band_of_casualty_label == '66 - 75' ? 10 : datum.age_band_of_casualty_label == 'Over 75' ? 11 : 99",
      "as": "age_order"
    }
  ],
  "mark": {"type": "bar", "cornerRadiusEnd": 2},
  "encoding": {
    "x": {
      "field": "age_band_of_casualty_label",
      "type": "ordinal",
      "title": "Nhóm tuổi",
      "sort": {"field": "age_order", "order": "ascending"},
      "axis": {"labelAngle": -35}
    },
    "y": {
      "field": "Total Casualties",
      "type": "quantitative",
      "title": "Số người thương vong",
      "axis": {"format": "~s"}
    },
    "xOffset": {
      "field": "Giới tính"
    },
    "color": {
      "field": "Giới tính",
      "type": "nominal",
      "title": "Giới tính",
      "scale": {
        "domain": ["Nam", "Nữ"],
        "range": ["#2563EB", "#EC4899"]
      },
      "legend": {"orient": "top", "direction": "horizontal"}
    },
    "tooltip": [
      {"field": "age_band_of_casualty_label", "title": "Nhóm tuổi"},
      {"field": "Giới tính", "title": "Giới tính"},
      {"field": "Total Casualties", "title": "Số người thương vong", "format": ","}
    ]
  }
}
```

---

## 4. Biểu đồ 4: Tỷ lệ mức độ thương vong theo vai trò

**Mục tiêu:** Không chỉ so sánh số lượng tuyệt đối, mà còn xem vai trò nào có tỷ trọng thương vong nặng cao hơn.

**Loại biểu đồ:** 100% Stacked Column Chart.

**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**

- `Casualties` > **`casualty_class_label`**
- `Casualties` > **`casualty_severity_label`**
- `Casualties` > **`Total Casualties`** (Measure)

**BƯỚC 2: COPY MÃ JSON VÀO SPECIFICATION**

```json
{
  "data": {"name": "dataset"},
  "title": {
    "text": "Tỷ lệ mức độ thương vong theo vai trò tham gia giao thông",
    "anchor": "middle",
    "fontSize": 15,
    "fontWeight": "bold",
    "dy": -5
  },
  "transform": [
    {
      "calculate": "datum.casualty_class_label == 'Driver or rider' ? 'Người điều khiển' : datum.casualty_class_label == 'Passenger' ? 'Hành khách' : datum.casualty_class_label == 'Pedestrian' ? 'Người đi bộ' : datum.casualty_class_label",
      "as": "Vai trò"
    },
    {
      "calculate": "datum.casualty_severity_label == 'Fatal' ? 'Tử vong' : datum.casualty_severity_label == 'Serious' ? 'Nghiêm trọng' : datum.casualty_severity_label == 'Slight' ? 'Nhẹ' : datum.casualty_severity_label",
      "as": "Mức độ thương vong"
    },
    {
      "calculate": "datum.casualty_severity_label == 'Fatal' ? 1 : datum.casualty_severity_label == 'Serious' ? 2 : datum.casualty_severity_label == 'Slight' ? 3 : 99",
      "as": "severity_order"
    }
  ],
  "mark": {"type": "bar"},
  "encoding": {
    "x": {
      "field": "Vai trò",
      "type": "nominal",
      "title": "Vai trò tham gia giao thông",
      "sort": ["Người điều khiển", "Hành khách", "Người đi bộ"],
      "axis": {"labelAngle": 0}
    },
    "y": {
      "field": "Total Casualties",
      "type": "quantitative",
      "stack": "normalize",
      "title": "Tỷ lệ thương vong",
      "axis": {"format": "%"}
    },
    "color": {
      "field": "Mức độ thương vong",
      "type": "nominal",
      "title": "Mức độ thương vong",
      "scale": {
        "domain": ["Tử vong", "Nghiêm trọng", "Nhẹ"],
        "range": ["#991B1B", "#FBBF24", "#2DD4BF"]
      },
      "legend": {"orient": "top", "direction": "horizontal"}
    },
    "order": {
      "field": "severity_order",
      "type": "quantitative",
      "sort": "ascending"
    },
    "tooltip": [
      {"field": "Vai trò", "title": "Vai trò"},
      {"field": "Mức độ thương vong", "title": "Mức độ"},
      {"field": "Total Casualties", "title": "Số người thương vong", "format": ","}
    ]
  }
}
```

---

## 5. Slicer và KPI nên dùng trên trang của Vinh

Để dashboard cá nhân trực quan nhưng không rối, chỉ nên dùng:

- `Calendar[Year]` làm slicer **Năm**.
- `Casualties[sex_of_casualty_label]` làm slicer **Giới tính**.
- KPI card: `[Total Casualties]`, đặt tên hiển thị là **Tổng số người thương vong**.

Không nên thêm slicer theo `casualty_severity_label`, `casualty_class_label` hoặc `age_band_of_casualty_label` trên cùng trang này, vì chính các trường đó đang là nội dung so sánh trong biểu đồ.

---

## 6. Checklist kiểm tra trước khi chụp hình

- [ ] Biểu đồ nhóm tuổi không còn nhóm `Data missing or out of range`.
- [ ] Nhóm tuổi được sort đúng thứ tự tự nhiên.
- [ ] Mức độ thương vong hiển thị tiếng Việt: `Tử vong`, `Nghiêm trọng`, `Nhẹ`.
- [ ] Vai trò hiển thị tiếng Việt: `Người điều khiển`, `Hành khách`, `Người đi bộ`.
- [ ] Màu không bị một màu duy nhất; các nhóm quan trọng có màu phân biệt rõ.
- [ ] Tooltip dùng tiêu đề tiếng Việt.
- [ ] KPI và slicer không che biểu đồ.
- [ ] Nếu chụp ảnh tổng quan, bỏ chọn filter riêng lẻ để số liệu quay về toàn bộ giai đoạn 2020-2024.

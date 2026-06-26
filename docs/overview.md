# HƯỚNG DẪN THIẾT LẬP DENEB (VEGA-LITE) TRONG POWER BI

Tài liệu này hướng dẫn cách sử dụng Custom Visual **Deneb** (sử dụng ngôn ngữ **Vega-lite**) trong Power BI Desktop. Mục tiêu là tạo ra các biểu đồ và KPI Card có giao diện đồng bộ với Dark Theme của đồ án Lab 03, sử dụng ĐÚNG các trường dữ liệu và Measures trong model (như đã quy định tại `dataset_description.md`).

---

## 1. Cài đặt và Thiết lập Deneb

1. Mở file Power BI `group15_base_model.pbix`.
2. Trong panel **Visualizations**, click vào dấu `...` (Get more visuals).
3. Tìm kiếm **Deneb** và chọn Add để thêm vào báo cáo.
4. Click vào icon Deneb vừa thêm để tạo một visual trống trên canvas.
5. **Kéo thả CHÍNH XÁC các trường dữ liệu (từ Data pane) vào mục Values của Deneb.** (Mỗi tài liệu mục tiêu sẽ liệt kê rõ cần kéo trường nào).
6. Click vào dấu `...` trên góc phải của visual Deneb trống, chọn **Edit** để mở trình soạn thảo (Editor).
7. Chọn Provider là **Vega-Lite**.

---

## 2. Cấu hình giao diện đồ họa Dark Theme (Config)

Để đồng bộ với giao diện của nhóm, hãy tab sang thẻ **Config** trong Deneb Editor và dán đoạn JSON sau (không dán vào thẻ Specification). Đoạn config này sẽ thiết lập nền màu `#0B0F19`, font chữ `sans-serif` trắng (`#FFFFFF`) và các thành phần trục phù hợp với Dark Mode:

```json
{
  "background": "#0B0F19",
  "view": {
    "stroke": "transparent"
  },
  "axis": {
    "domainColor": "#334155",
    "gridColor": "#334155",
    "tickColor": "#334155",
    "labelColor": "#94A3B8",
    "titleColor": "#FFFFFF",
    "labelFont": "sans-serif",
    "titleFont": "sans-serif"
  },
  "legend": {
    "labelColor": "#94A3B8",
    "titleColor": "#FFFFFF",
    "labelFont": "sans-serif",
    "titleFont": "sans-serif"
  },
  "title": {
    "color": "#FFFFFF",
    "subtitleColor": "#94A3B8",
    "font": "sans-serif",
    "subtitleFont": "sans-serif"
  },
  "text": {
    "font": "sans-serif",
    "color": "#FFFFFF"
  }
}
```

---

## 3. Hướng dẫn tạo KPI Card bằng Vega-lite

Dưới đây là mã JSON Vega-lite để hiển thị thẻ KPI cho Measure **Total Casualties**.

**BƯỚC 1: KÉO DỮ LIỆU VÀO VALUES**
- `Casualties` > **`Total Casualties`** (Measure)

**BƯỚC 2: COPY MÃ JSON DƯỚI ĐÂY VÀO THẺ SPECIFICATION**
```json
{
  "data": {"name": "dataset"},
  "layer": [
    {
      "mark": {
        "type": "text",
        "fontSize": 48,
        "fontWeight": "bold",
        "color": "#FFFFFF",
        "align": "center",
        "baseline": "bottom",
        "dy": -10
      },
      "encoding": {
        "text": {"field": "Total Casualties", "type": "quantitative", "format": ","}
      }
    },
    {
      "mark": {
        "type": "text",
        "fontSize": 16,
        "color": "#94A3B8",
        "align": "center",
        "baseline": "top"
      },
      "encoding": {
        "text": {"value": "Total Casualties"}
      }
    }
  ]
}
```

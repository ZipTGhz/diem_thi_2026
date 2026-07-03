# Bộ Dữ Liệu Điểm Thi THPT 2026 (Format .jsonl)

Kho lưu trữ và chia sẻ toàn bộ dữ liệu điểm thi tốt nghiệp THPT năm 2026 tại Việt Nam.

---

## Cấu Trúc Thư Mục

Dữ liệu được chia nhỏ và đặt tên không dấu theo thư mục phân loại tỉnh thành để thuận tiện cho việc tải hoặc xử lý riêng lẻ từng địa phương:

```text
.
├── city_category/
│   ├── 01_Ha_Noi.jsonl
│   ├── 04_Cao_Bang.jsonl
│   ├── 08_Tuyen_Quang.jsonl
│   ├── ...
│   ├── 92_Can_Tho.jsonl
│   └── 96_Ca_Mau.jsonl
└── README.md
```

## Cấu Trúc Bản Ghi (Data Schema)

Mỗi dòng trong file .jsonl đại diện cho dữ liệu điểm thi của một thí sinh, định dạng theo cấu trúc key-value rõ ràng. Các môn thí sinh không dự thi sẽ không được liệt kê.

Ví dụ vài dòng dữ liệu mẫu: \
{"01129161": {"Môn Toán": "5.75", "Môn Văn": "6.75", "Môn Lý": "3", "Môn Ngoại ngữ": "5"}} \
{"52001575": {"Môn Toán": "7.5", "Môn Lý": "9", "Môn Hóa": "5.6"}}\
{"01000006": {"Môn Văn": "8.25"}}

## Gợi ý đọc dữ liệu bằng Python

```python
import json
import pandas as pd

file_path = 'city_category/01_Ha_Noi.jsonl'
records = []

with open(file_path, 'r', encoding='utf-8') as f:
    for line in f:
        line_str = line.strip()
        if not line_str:
            continue

        data = json.loads(line_str)
        for sbd, mon_thi in data.items():
            row = {"SBD": sbd}
            row.update(mon_thi)
            records.append(row)

df = pd.DataFrame(records)
print(df.head())
```

## Giấy Phép (License)
Dự án được chia sẻ dưới giấy phép MIT License - Hoàn toàn tự do sử dụng cho mục đích học tập, nghiên cứu và thống kê giáo dục phi thương mại.

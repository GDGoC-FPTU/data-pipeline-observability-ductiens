[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-2e0aaae1b6195c2367325f4f02e2d04e9abb55f0b24a779b69b11b9e10269abc.svg)](https://classroom.github.com/online_ide?assignment_repo_id=23573938&assignment_repo_type=AssignmentRepo)

# Day 10 Lab: Data Pipeline & Data Observability

**Student Email:** carina.ndt@gmail.com
**Name:** Nguyễn Đức Tiến

---

## Mo ta

(Mo ta ngan gon bai lab va nhung gi ban da lam)

Dự án này xây dựng một pipeline ETL đơn giản để:

- Extract dữ liệu sản phẩm từ file `raw_data.json`.
- Validate và loại bỏ các bản ghi không hợp lệ như giá <= 0 hoặc category trống.
- Transform dữ liệu bằng cách chuẩn hóa `category` và tính `discounted_price`.
- Load kết quả ra file `processed_data.csv` cùng cột `processed_at`.

---

## Cach chay (How to Run)

### Prerequisites

```bash
pip install pandas
```

### Chay ETL Pipeline

```bash
python solution.py
```

### Chay Agent Simulation (Stress Test)

```bash
# Mo ta cach ban chay thi nghiem Clean vs Garbage data
# Mở terminal trong thư mục dự án
python agent_simulation.py
```

Sau khi chạy, kiểm tra output cho hai trường hợp:

- `processed_data.csv` (Clean Data)
- `garbage_data.csv` (Garbage Data)

---

## Cau truc thu muc

```
├── solution.py              # ETL Pipeline script
├── processed_data.csv       # Output cua pipeline
├── experiment_report.md     # Bao cao thi nghiem
└── README.md                # File nay
```

---

## Ket qua

(Tom tat ket qua: bao nhieu records da xu ly, bao nhieu bi loai, v.v.)

Kết quả hiện tại:

- File `processed_data.csv` chứa 3 bản ghi hợp lệ được giữ lại sau khi validate.
- `solution.py` loại bỏ các bản ghi có `price` <= 0 hoặc `category` trống.
- `agent_simulation.py` chứng minh rằng dữ liệu sạch dẫn đến kết quả agent chính xác hơn, trong khi dữ liệu nhiễu (garbage data) gây ra lựa chọn sai do outlier và giá trị không hợp lệ.

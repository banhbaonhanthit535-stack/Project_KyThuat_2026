# 🎓 DỰ ÁN PHÂN TÍCH MỨC ĐỘ CẠNH TRANH VÀ DỰ BÁO ĐIỂM CHUẨN ĐẠI HỌC KHỐI CÔNG NGHỆ – KỸ THUẬT (2023–2026)

> **Học phần:** Phân tích Dữ liệu Nâng cao (ADY201m) – Trường Đại học Công nghệ  
> **Lĩnh vực:** Giáo dục & Khoa học Dữ liệu Tuyển sinh Đại học  
> **Quy mô dữ liệu:** 4.292.528 Thí sinh THPT | 13.120 Điểm chuẩn | 3.360 Chỉ tiêu | 36 Trường Đại học Hà Nội  

---

## 📌 1. Giới thiệu Đề tài & Bối cảnh Nghiên cứu
Dự án giải quyết bài toán tuyển sinh đại học trong giai đoạn chuyển giao quy chế thi tốt nghiệp THPT từ năm 2025 theo Chương trình GDPT 2018 (thi 4 môn, xuất hiện môn Tin học và tổ hợp mới `X06, X26`). Hệ thống xây dựng một đường ống Khoa học Dữ liệu thực chiến khép kín (**End-to-End Pipeline**) từ thiết kế kho CSDL SQL Server, làm sạch đồng bộ chuỗi dữ liệu, chế biến 16 đặc trưng chống rò rỉ, huấn luyện học máy tăng cường đến triển khai ứng dụng Web Dashboard tư vấn 3 nhóm nguyện vọng.

---

## 🚀 2. Điểm Nhấn Công Nghệ & Kết Quả Đạt Được

* **Hạ tầng CSDL SQL Server `ady` (12 Bảng):** Tiếp nhận hơn 4,29 triệu bản ghi thí sinh, đóng gói bảng bộ nhớ đệm `ThongKePhoDiem_Cache` giúp truy vấn đặc trưng tức thời dưới 0.05s.
* **Làm sạch 2 tầng & So khớp `difflib`:** Quy đổi thang 40 về thang 30, lọc bỏ trùng lặp cơ sở phía Nam (còn 13.120 dòng sạch) và đồng bộ 242 tên ngành viết lệch giữa Chỉ tiêu và Điểm chuẩn với ngưỡng `cutoff = 0.90`.
* **Mô hình AI Đề xuất (3 Nhóm Chuyên gia `HistGradientBoostingRegressor` kép):**
  * Đạt **$R^2 = 0.7352$** (giải thích 73.52% sự biến thiên điểm chuẩn), sai số tuyệt đối trung bình **$\text{MAE} = 1.0196$ điểm** và sai số trung vị **$\text{MedAE} = 0.7223$ điểm** trên tập kiểm thử độc lập năm 2025 ($n = 151$).
  * Vượt trội hoàn toàn mô hình nền Linear Regression ($R^2 = -25.1010, \text{MAE} = 10.98$ điểm) và Cây quyết định đơn ($R^2 = 0.7062$).
* **Chỉ số Cạnh tranh Tuyển sinh Đa biến ($\text{CI}$ thang 0 – 100):**
  $$\text{CI} = 0.50 \cdot \text{diem\_norm} + 0.25 \cdot \text{ty\_le\_choi\_norm} + 0.15 \cdot \text{tier\_norm} + 0.10 \cdot \text{xu\_huong\_norm}$$
  Phân tầng khách quan 216 ngành công nghệ năm 2026: **54 ngành Rất cao (25%)**, **70 ngành Cao (32.4%)**, **68 ngành Trung bình (31.5%)** và **24 ngành Thấp (11.1%)**.
* **Web App Streamlit (`app.py`, `run.bat`):** Chạy Offline 100% không phụ thuộc Internet, tự động phân 3 Tab Nguyện vọng: **Nhóm An Toàn** ($\Delta \ge +0.5$đ), **Nhóm Vừa Sức** ($\pm 0.5$đ) và **Nhóm Thử Thách** ($\Delta < -0.5$đ).

---

## 📂 3. Cấu Trúc Thư Mục Repository

```
├── báo cáo dự án/
│   ├── BAO_CAO_DO_AN_ADY201M.docx      # Quyển Báo cáo Word hoàn chỉnh chuẩn format học thuật
│   ├── BAO_CAO_DO_AN_ADY201M.md        # Toàn văn Báo cáo dạng Markdown chi tiết
│   ├── 1. Problem Formulation and Approach.ipynb
│   ├── 2. Database Schema and Score Distribution.ipynb
│   ├── 3. Data Collection and Quality Assessment.ipynb
│   ├── 4. SQL Data Cleaning and Synchronization.ipynb
│   ├── 5. Feature Engineering and Competition EDA.ipynb
│   ├── 6. Cutoff and Competition Modeling.ipynb
│   ├── 7. Admission Advisory Web App and Conclusion.ipynb
│   └── images/                         # 7 biểu đồ và sơ đồ ERD độ phân giải cao
├── data_clean/                         # Dữ liệu sạch đã chế biến đặc trưng (0% khuyết)
│   ├── du_lieu_cong_nghe_full.csv      # 478 chương trình Công nghệ 2023–2025
│   ├── tap_hoc_train_2023_2024.csv     # Tập Train 262 dòng
│   └── tap_kiem_thu_test_2025.csv      # Tập Test độc lập 151 dòng
├── data_raw/                           # Dữ liệu tham chiếu đầu vào nhẹ
│   ├── Chỉ tiêu.xlsx                   # Chỉ tiêu tuyển sinh 3.360 dòng
│   ├── Tier list.xlsx                  # Bảng phân hạng 36 trường ĐH
│   ├── trend_nganh_google.csv          # Dữ liệu Google Trends 2021–2026
│   └── README.md                       # Hướng dẫn tải 4 tệp điểm thi THPT gốc (>25MB)
├── models/
│   └── ultimate_model.pkl              # Bộ mô hình AI kép đã đóng gói sẵn sàng demo
├── results/
│   ├── predictions_2026.csv            # Bảng dự báo 216 ngành 2026 kèm Chỉ số CI
│   └── school_mapping.json             # Từ điển 36 trường đại học Hà Nội
├── src/                                # Thư viện mã nguồn lõi của dự án
│   ├── data_processing.py              # Tiền xử lý dữ liệu và tạo 16 đặc trưng
│   ├── model_training.py               # Huấn luyện 3 Nhóm Chuyên gia AI & Blending
│   └── prediction.py                   # Suy luận dự báo điểm và tính Chỉ số CI
├── 1_import_data_to_sql.py             # Kịch bản nạp điểm thi vào SQL Server
├── 2_scrape_diemchuan.py               # Cào điểm chuẩn lịch sử từ API
├── 3_scrape_chitieu.py                 # Chuẩn hóa nạp chỉ tiêu tuyển sinh
├── 4_data_cleaning.py                  # Làm sạch và đồng bộ CSDL SQL Server
├── 5_train_model.py                    # Bộ điều phối huấn luyện và xuất dự báo
├── app.py                              # Ứng dụng Web Dashboard Streamlit
├── config.py                           # Cấu hình chuỗi kết nối SQL Server
├── schema.sql, Procedures.sql, run_data.sql # Tệp khởi tạo và thủ tục SQL Server
├── run.bat                             # Phím tắt khởi chạy nhanh Web App
└── requirements.txt                    # Danh sách thư viện Python cần thiết
```

---

## ⚡ 4. Hướng Dẫn Cài Đặt & Chạy Web App

1. **Khởi chạy nhanh (Khuyến nghị trên Windows):**
   * Nhấp đúp chuột vào file `run.bat` ở thư mục gốc. Trình duyệt web sẽ tự động mở giao diện tư vấn tại `http://localhost:8501`.

2. **Khởi chạy thủ công qua dòng lệnh:**
   ```bash
   pip install -r requirements.txt
   streamlit run app.py
   ```

---
*Dự án hoàn thành phục vụ đánh giá cuối kỳ môn Phân tích Dữ liệu Nâng cao (ADY201m) - Năm 2026.*

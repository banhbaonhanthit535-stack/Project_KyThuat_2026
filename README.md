# DỰ ÁN PHÂN TÍCH MỨC ĐỘ CẠNH TRANH VÀ DỰ BÁO ĐIỂM CHUẨN ĐẠI HỌC KHỐI CÔNG NGHỆ – KỸ THUẬT (2023–2026)

> **Học phần:** Phân tích Dữ liệu Nâng cao (ADY201m)  
> **Lĩnh vực nghiên cứu:** Khoa học Dữ liệu và Phân tích Giáo dục Đại học  
> **Quy mô dữ liệu:** 4.292.528 Thí sinh THPT | 13.120 Bản ghi Điểm chuẩn | 3.360 Chỉ tiêu | 36 Trường Đại học Khu vực Hà Nội  

---

## 1. Giới thiệu đề tài và bối cảnh nghiên cứu

Dự án giải quyết bài toán tuyển sinh đại học trong giai đoạn chuyển giao quy chế thi tốt nghiệp THPT từ năm 2025 theo Chương trình Giáo dục phổ thông 2018 (kỳ thi 4 môn, xuất hiện môn Tin học và các tổ hợp mới X06, X26). 

Đề tài xây dựng quy trình Khoa học Dữ liệu khép kín (End-to-End Data Science Pipeline):
1. **Thiết kế hạ tầng:** Kho cơ sở dữ liệu quan hệ SQL Server chuẩn hóa lưu trữ hàng triệu bản ghi thí sinh.
2. **Tiền xử lý và đồng bộ:** Chuẩn hóa thang điểm, đồng bộ danh mục ngành và xử lý dị biệt chuỗi thời gian.
3. **Kỹ thuật đặc trưng (Feature Engineering):** Trích xuất 16 đặc trưng phản ánh phổ điểm, biến động chỉ tiêu và áp lực cạnh tranh không rò rỉ thông tin tương lai.
4. **Mô hình hóa (Machine Learning):** Ứng dụng kiến trúc kết hợp đa mô hình học máy tăng cường gradient (HistGradientBoostingRegressor) chia theo 3 nhóm chuyên gia lĩnh vực.
5. **Xây dựng chỉ số định lượng:** Thiết lập Chỉ số Cạnh tranh Tuyển sinh Đa biến (Competition Index - CI) phản ánh độ khốc liệt thực tế.
6. **Triển khai ứng dụng:** Dashboard phân tích và tư vấn danh mục nguyện vọng trực quan phục vụ thí sinh và phụ huynh.

---

## 2. Kết quả đạt được và đóng góp kỹ thuật

* **Hạ tầng CSDL SQL Server (12 Bảng chuẩn hóa):** Tiếp nhận và lập chỉ mục tối ưu hơn 4,29 triệu bản ghi thí sinh THPT; xây dựng bảng đệm `ThongKePhoDiem_Cache` phục vụ trích xuất đặc trưng phân vị điểm với độ trễ dưới 0.05 giây.
* **Làm sạch và đồng bộ chuỗi thời gian đa nguồn:** Quy đổi thống nhất điểm chuẩn thang 40 về thang 30 chuẩn; ứng dụng thuật toán so khớp chuỗi xấp xỉ `difflib` với ngưỡng cutoff 0.90 để đồng bộ 242 tên ngành giữa Đề án tuyển sinh và Điểm chuẩn trúng tuyển.
* **Mô hình học máy dự báo điểm chuẩn (3 Nhóm Chuyên gia HistGradientBoostingRegressor kép):**
  * Hệ số xác định $R^2 = 0.7352$ (giải thích 73.52% sự biến thiên của điểm chuẩn trúng tuyển năm chuyển giao 2025 trên tập kiểm thử độc lập gồm 151 chương trình đào tạo).
  * Sai số tuyệt đối trung bình $\text{MAE} = 1.0196$ điểm, sai số tuyệt đối trung vị $\text{MedAE} = 0.7223$ điểm.
  * Hiệu năng vượt trội đáng kể so với mô hình tham chiếu Hồi quy tuyến tính ($\text{MAE} = 10.98$ điểm) và Cây quyết định đơn ($\text{MAE} = 1.1063$ điểm).
* **Chỉ số Cạnh tranh Tuyển sinh Đa biến (Competition Index - CI, thang 0 – 100):**

  $$
  \text{CI} = 0.50 \times \text{Score}_{\text{norm}} + 0.25 \times \text{Ratio}_{\text{norm}} + 0.15 \times \text{Tier}_{\text{norm}} + 0.10 \times \text{Trend}_{\text{norm}}
  $$

  *Trong đó các thành phần được chuẩn hóa Min-Max: Điểm chuẩn (50%), Tỷ lệ chọi (25%), Phân hạng trường (15%), Xu hướng quan tâm Google Trends (10%).*

  Phân tầng khách quan 216 chương trình đào tạo công nghệ năm 2026: **54 ngành Rất cao (25.0%)**, **70 ngành Cao (32.4%)**, **68 ngành Trung bình (31.5%)** và **24 ngành Thấp (11.1%)**.
* **Ứng dụng tư vấn tuyển sinh (Streamlit Dashboard):** Triển khai cục bộ ổn định, cung cấp chức năng đối sánh tự động 3 phân nhóm nguyện vọng: Nhóm An toàn ($\Delta \ge +0.5$ điểm), Nhóm Vừa sức ($\pm 0.5$ điểm) và Nhóm Thử thách ($\Delta < -0.5$ điểm).

---

## 3. Cấu trúc thư mục dự án

```
├── báo cáo dự án/
│   ├── BAO_CAO_DO_AN_ADY201M.docx      # Báo cáo tổng kết đồ án (Định dạng Word học thuật)
│   ├── BAO_CAO_DO_AN_ADY201M.md        # Toàn văn báo cáo tổng kết dạng Markdown
│   ├── 1. Problem Formulation and Approach.ipynb
│   ├── 2. Database Schema and Score Distribution.ipynb
│   ├── 3. Data Collection and Quality Assessment.ipynb
│   ├── 4. SQL Data Cleaning and Synchronization.ipynb
│   ├── 5. Feature Engineering and Competition EDA.ipynb
│   ├── 6. Cutoff and Competition Modeling.ipynb
│   ├── 7. Admission Advisory Web App and Conclusion.ipynb
│   └── images/                         # Biểu đồ phân tích và sơ đồ kiến trúc hệ thống
├── data_clean/                         # Dữ liệu sạch phục vụ huấn luyện mô hình
│   ├── du_lieu_cong_nghe_full.csv      # 478 chương trình Công nghệ giai đoạn 2023–2025
│   ├── tap_hoc_train_2023_2024.csv     # Tập huấn luyện (262 bản ghi)
│   └── tap_kiem_thu_test_2025.csv      # Tập kiểm thử độc lập (151 bản ghi)
├── data_raw/                           # Dữ liệu thô và tài liệu tham chiếu đầu vào
│   ├── Chỉ tiêu.xlsx                   # Đề án chỉ tiêu tuyển sinh (3.360 bản ghi)
│   ├── Tier list.xlsx                  # Bảng phân hạng 36 cơ sở giáo dục đại học
│   ├── trend_nganh_google.csv          # Dữ liệu xu hướng tìm kiếm Google Trends
│   ├── diem_thpt_2023.csv              # Dữ liệu mẫu điểm thi THPT 2023 (5.000 dòng)
│   ├── diem_thpt_2024.csv              # Dữ liệu mẫu điểm thi THPT 2024 (5.000 dòng)
│   ├── diem_thpt_2025.csv              # Dữ liệu mẫu điểm thi THPT 2025 (5.000 dòng)
│   ├── diem_thpt_2026.csv              # Dữ liệu mẫu điểm thi THPT 2026 (5.000 dòng)
│   └── README.md                       # Ghi chú hướng dẫn liên kết dữ liệu gốc
├── models/
│   └── ultimate_model.pkl              # Mô hình học máy đã huấn luyện đóng gói
├── results/
│   ├── predictions_2026.csv            # Kết quả dự báo 216 ngành năm 2026 kèm Chỉ số CI
│   └── school_mapping.json             # Danh mục đối chiếu 36 trường đại học Hà Nội
├── src/                                # Thư viện xử lý thuật toán cốt lõi
│   ├── data_processing.py              # Tiền xử lý dữ liệu và trích xuất đặc trưng
│   ├── model_training.py               # Huấn luyện mô hình và tối ưu hóa trọng số
│   └── prediction.py                   # Bộ suy luận dự báo và tính toán chỉ số CI
├── 1_import_data_to_sql.py             # Kịch bản nạp dữ liệu điểm thi vào CSDL SQL Server
├── 2_scrape_diemchuan.py               # Kịch bản thu thập điểm chuẩn lịch sử
├── 3_scrape_chitieu.py                 # Chuẩn hóa dữ liệu đề án tuyển sinh
├── 4_data_cleaning.py                  # Quy trình làm sạch và đồng bộ cơ sở dữ liệu
├── 5_train_model.py                    # Thực thi huấn luyện và xuất kết quả dự báo
├── app.py                              # Giao diện ứng dụng bảng điều khiển Streamlit
├── config.py                           # Thiết lập tham số hệ thống và kết nối CSDL
├── schema.sql, Procedures.sql, run_data.sql # Tệp kịch bản định nghĩa và khởi tạo CSDL
├── run.bat                             # Kịch bản khởi chạy nhanh ứng dụng giao diện
└── requirements.txt                    # Danh sách các thư viện phụ thuộc
```

---

## 4. Hướng dẫn cài đặt và thực thi

1. **Khởi chạy ứng dụng bảng điều khiển (Khuyến nghị trên Windows):**
   * Khởi chạy tệp `run.bat` tại thư mục gốc. Ứng dụng sẽ tự động mở trên trình duyệt tại địa chỉ mặc định `http://localhost:8501`.

2. **Khởi chạy thông qua môi trường dòng lệnh:**
   ```bash
   pip install -r requirements.txt
   streamlit run app.py
   ```

---
*Báo cáo dự án học phần Phân tích Dữ liệu Nâng cao (ADY201m).*

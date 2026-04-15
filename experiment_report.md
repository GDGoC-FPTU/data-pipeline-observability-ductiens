# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** AI20K-2A202600393
**Name:** Nguyễn Đức Tiến
**Date:** 15/04/2026

---

## 1. Ket qua thi nghiem

Chay `agent_simulation.py` voi 2 bo du lieu va ghi lai ket qua:

| Scenario                          | Agent Response                                                          | Accuracy (1-10) | Notes                                                                             |
| --------------------------------- | ----------------------------------------------------------------------- | --------------- | --------------------------------------------------------------------------------- |
| Clean Data (`processed_data.csv`) | Agent: Based on my data, the best choice is Laptop at $1200.            | 9/10            | Dữ liệu sạch, chỉ gồm sản phẩm điện tử hợp lệ.                                    |
| Garbage Data (`garbage_data.csv`) | Agent: Based on my data, the best choice is Nuclear Reactor at $999999. | 3/10            | Dữ liệu nhiễu chứa outlier, giá sai định dạng, ID trùng và trường category thiếu. |

---

## 2. Phan tich & nhan xet

### Tai sao Agent tra loi sai khi dung Garbage Data?

(Viet nhan xet cua ban o day — it nhat 50 tu)
Trong trường hợp dữ liệu sạch, agent chọn đúng sản phẩm điện tử có giá cao nhất từ `processed_data.csv` vì mô phỏng dựa trên logic tìm giá tốt nhất trong category electronics. Dữ liệu đã được xử lý, loại bỏ các bản ghi không hợp lệ, chuẩn hóa `category` và thêm chỉ số `processed_at`, nên agent có thể hoạt động chính xác.

Khi dùng `garbage_data.csv`, dữ liệu chứa nhiều lỗi: một bản ghi có `price` là chuỗi "ten dollars", một bản ghi thiếu `id`, một bản ghi có `price` bằng 0 và không có `category`, và một bản ghi có ID trùng lặp. Quan trọng nhất, tồn tại outlier lớn `Nuclear Reactor` với giá `999999` và category đúng là `electronics`, nên agent ghi nhận đó là lựa chọn tốt nhất theo logic hiện tại. Điều này cho thấy agent không chỉ bị ảnh hưởng bởi lỗi dữ liệu mà còn bị lệ thuộc vào phép so sánh giá và không có kiểm tra chất lượng sâu hơn.

(Hay phan tich cac van de nhu Duplicate IDs, wrong data types, outliers, null values
va giai thich tai sao chung anh huong den ket qua cua Agent.)

- Duplicate IDs: có thể khiến dữ liệu không nhất quán và làm sai lệch thống kê nếu agent hoặc hệ thống tính trung bình, phân nhóm.
- Wrong data types: giá trị `"ten dollars"` không thể chuyển thành số và nếu không xử lý đúng sẽ làm script hoặc mô phỏng trả về lỗi.
- Outliers: giá trị cực lớn `999999` đánh lừa logic chọn sản phẩm tốt nhất, dù rõ ràng không phải lựa chọn hợp lý cho người dùng thông thường.
- Null values / missing fields: sản phẩm thiếu category hoặc giá 0 không nên được đưa vào cơ sở dữ liệu dùng cho quyết định.

Từ đó, ta thấy dữ liệu xấu làm agent đưa ra đáp án sai hoặc ít giá trị, ngay cả khi prompt vẫn giống nhau. Prompt tốt không bù được hoàn toàn dữ liệu bị nhiễu và không chính xác.

---

## 3. Ket luan

**Quality Data > Quality Prompt?** Đồng ý

(Viet ket luan cua ban o day)
Dữ liệu chất lượng cao là nền tảng quan trọng hơn vì agent chỉ có thể suy luận đúng khi nguồn dữ liệu đầu vào đáng tin cậy. Prompt tốt giúp định hướng, nhưng nếu dữ liệu bị lỗi, trùng lặp, hoặc chứa nhiễu, thì kết quả vẫn có thể sai.

Dữ liệu sạch và observability là yếu tố quyết định để bảo đảm agent đưa ra lựa chọn chính xác, còn prompt chỉ giúp khai thác dữ liệu đã có một cách hiệu quả hơn.

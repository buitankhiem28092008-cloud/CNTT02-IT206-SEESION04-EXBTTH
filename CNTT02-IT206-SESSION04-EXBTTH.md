# [BTTH] Bài tập thực hành tổng hợp
## 1. Báo cáo thiết kế giải pháp (Solution Design)
**Bài toán yêu cầu xử lý một quy trình tự động hóa phức tạp: Tiếp nhận phản hồi tiêu cực của khách hàng, phân tích nguyên nhân gốc rễ, và soạn email xin lỗi/đền bù tự động.**

**Để giải quyết, hệ thống áp dụng kiến trúc Prompt Chaining (Chuỗi Prompt tuần tự) kết hợp Chain-of-Thought (Chuỗi tư duy) và cơ chế Fallbacks (Bắt lỗi đứt gãy)**
- [x] Bước 1 (Extraction & Validation): Trích xuất thông tin thô từ phản hồi của khách hàng và kiểm tra tính hợp lệ (bắt dữ liệu thiếu/dị biệt để không làm crash hệ thống).
- [x] Bước 2 (Root Cause Analysis - CoT): Suy luận logic từng bước để tìm nguyên nhân gốc rễ của sự cố dựa trên dữ liệu đã chuẩn hóa.
- [x] Bước 3 (Action & Response Generation): Dựa vào kết quả bước 2 để đưa ra mức đền bù phù hợp và sinh nội dung email phản hồi chuyên nghiệp.
## 2. Hệ thống Prompt thực thi các bước
**Bước 1: Prompt Trích xuất & Kiểm tra dữ liệu (Validation & Extraction)**
Bạn là một bộ tiền xử lý dữ liệu thông minh. Hãy trích xuất thông tin từ phản hồi của khách hàng dưới đây thành định dạng JSON chuẩn.
Nếu thông tin nào bị thiếu, hãy điền là null. Nếu phát hiện dữ liệu vô lý hoặc dị biệt (ví dụ: ngày tháng tương lai, sai định dạng nghiêm trọng), hãy gán status là "ERROR".

Dữ liệu đầu vào: {noi_dung_khach_hang}

Đầu ra bắt buộc là JSON thuần túy theo cấu trúc:
{
  "extracted": {
    "ten_khach": "...",
    "ma_don_hang": "...",
    "van_de_gap_phai": "..."
  },
  "status": "VALID" hoặc "ERROR"
}
**Bước 2: Prompt Phân tích nguyên nhân (Chain-of-Thought)**
Bạn là chuyên gia phân tích chất lượng dịch vụ. Hãy sử dụng tư duy từng bước (Chain-of-Thought) để phân tích vấn đề của khách hàng từ dữ liệu đầu vào.

Dữ liệu: {json_tu_buoc_1}

Hãy thực hiện:
1. Suy luận nguyên nhân sâu xa dẫn đến lỗi (vận chuyển, lỗi hệ thống hay lỗi nhân sự).
2. Đánh giá mức độ nghiêm trọng (Thấp / Trung bình / Cao).

Trả về kết quả dưới dạng JSON:
{
  "reasoning_steps": ["Bước 1...", "Bước 2..."],
  "nguyen_nhan_goc_re": "...",
  "muc_do": "..."
}
**Bước 3: Prompt Sinh phản hồi khách hàng (Action & Response)**
Bạn là Trưởng bộ phận Chăm sóc Khách hàng. Dựa vào kết quả phân tích nguyên nhân, hãy soạn một email xin lỗi khách hàng lịch sự, chân thành kèm chính sách đền bù phù hợp.

Dữ liệu phân tích: {json_tu_buoc_2}

Yêu cầu:
- Ngôn từ thấu cảm, chuyên nghiệp.
- Đưa ra giải pháp khắc phục cụ thể.
- Trả về định dạng Markdown.
## 3. Kết quả chạy thử mẫu (Sample Output)
![alt text](image-1.png)
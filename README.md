#  RAG on YouTube Transcript with Gemini 1.5

##  Giới thiệu
Dự án này tập trung vào việc **áp dụng và hiểu cách hoạt động của RAG (Retrieval-Augmented Generation)**.  
Thay vì để mô hình LLM phải nhớ tất cả thông tin, ta sẽ xây dựng pipeline cho phép mô hình **truy xuất thông tin từ nguồn dữ liệu ngoài**, sau đó mới sinh câu trả lời.  

Trong dự án này, nguồn dữ liệu chính là **transcript (lời thoại) của video YouTube**, được thu thập trước đó. Từ dữ liệu văn bản này, ta tích hợp với **LLM Gemini 1.5** để tạo nên hệ thống hỏi đáp thông minh, dựa trực tiếp trên nội dung của video.

---

##  Quy trình hoạt động
1. **Lấy transcript của video YouTube**  
   - Sử dụng `youtube-transcript-api` để thu thập lời thoại của video.
   - Lưu dữ liệu thành văn bản thô để xử lý sau.

2. **Xử lý và chia nhỏ dữ liệu**  
   - Sử dụng kỹ thuật text splitting (ví dụ `RecursiveCharacterTextSplitter`) để chia transcript thành các đoạn nhỏ.
   - Mục đích: giúp cho việc tìm kiếm và truy xuất thông tin chính xác hơn.

3. **Xây dựng kho dữ liệu (Vector Database)**  
   - Chuyển các đoạn văn bản thành vector embeddings.
   - Lưu trữ trong vector DB để phục vụ việc tìm kiếm ngữ nghĩa.

4. **Kết nối với Gemini 1.5**  
   - Khi người dùng đặt câu hỏi, hệ thống sẽ truy vấn vector DB để tìm những đoạn transcript phù hợp.
   - Các đoạn văn bản được trả về sẽ được gửi kèm vào prompt cho
   - Gemini 1.5 sinh ra câu trả lời dựa trên.


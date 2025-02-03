# Groq Deep Researcher

Groq Deep Researcher là một trợ lý nghiên cứu web hoàn toàn tự động, sử dụng bất kỳ mô hình LLM nào được cung cấp bởi [Groq](https://groq.com/). Người dùng chỉ cần cung cấp một chủ đề, hệ thống sẽ tạo truy vấn tìm kiếm web, thu thập kết quả từ web (mặc định sử dụng [Tavily](https://www.tavily.com/)), tóm tắt thông tin thu thập được, phân tích lỗ hổng kiến thức, tạo truy vấn mới để bổ sung thông tin còn thiếu, và tiếp tục cải thiện bản tóm tắt trong số vòng lặp do người dùng định nghĩa. Cuối cùng, hệ thống sẽ cung cấp một tệp markdown tổng hợp nghiên cứu với tất cả các nguồn đã sử dụng.

![research-rabbit](https://github.com/user-attachments/assets/4308ee9c-abf3-4abb-9d1e-83e7c2c3f187)

Tóm tắt nhanh:
<video src="https://github.com/user-attachments/assets/02084902-f067-4658-9683-ff312cab7944" controls></video>

## 📺 Hướng dẫn video

Xem hệ thống hoạt động hoặc tự xây dựng nó? Hãy xem các hướng dẫn video hữu ích sau:
- [Building a fully local "deep researcher" with DeepSeek-R1](https://www.youtube.com/watch?v=sGUjmyfof4Q)
- Tải và thử nghiệm [DeepSeek R1](https://api-docs.deepseek.com/news/news250120).
- [Building a fully local research assistant from scratch with Ollama](https://www.youtube.com/watch?v=XGuTzHoqlj8) - Tổng quan về cách hệ thống được xây dựng.

## 🚀 Bắt đầu nhanh

### Mac / Windows

1. **Clone repository:**
   ```bash
   git clone https://github.com/thanh-abaii/groq-deep-researcher.git
   cd groq-deep-researcher
   ```

2. **Cấu hình biến môi trường**
   - Copy file `.env.example` thành `.env`:
   ```bash
   cp .env.example .env
   ```
   - Mở file `.env` bằng trình soạn thảo và **thêm API key của Groq**:
   ```bash
   # Required: API Key for Groq
   GROQ_API_KEY=your_groq_api_key  # Đăng ký API tại https://groq.com/
   
   # Optional: Web search provider
   TAVILY_API_KEY=tvly-xxxxx      
   PERPLEXITY_API_KEY=pplx-xxxxx  
   ```
   **Lưu ý:** Nếu bạn muốn đặt biến môi trường trực tiếp từ terminal:
   ```bash
   export GROQ_API_KEY=your_groq_api_key
   ```

3. **Tạo môi trường ảo Python (Khuyến nghị)**
   ```bash
   python -m venv .venv
   source .venv/bin/activate  # macOS/Linux
   .venv\Scripts\Activate.ps1  # Windows
   ```

4. **Cài đặt các thư viện cần thiết**
   ```bash
   pip install -e .
   pip install langgraph-cli[inmem]
   ```

5. **Khởi động assistant với LangGraph Server**
   ```bash
   langgraph dev
   ```

### 📌 Cách hoạt động

- **Trước đây (Ollama):** Mô hình được tải về và chạy cục bộ.
- **Bây giờ (Groq API):** Mô hình sẽ được gọi qua API của **Groq** thay vì chạy trên máy.

Cách hoạt động:
- Người dùng cung cấp chủ đề nghiên cứu.
- Mô hình LLM (gọi qua **Groq API**) tạo truy vấn tìm kiếm web.
- Công cụ tìm kiếm (Tavily hoặc Perplexity) thu thập dữ liệu từ web.
- LLM tóm tắt kết quả tìm kiếm và xác định khoảng trống kiến thức.
- Quá trình tìm kiếm lặp lại để bổ sung thông tin cần thiết.
- Kết quả cuối cùng là một tệp markdown chứa tóm tắt nghiên cứu với nguồn trích dẫn.

### 🎯 Sử dụng LangGraph Studio UI

Khi khởi động **LangGraph Server**, bạn sẽ thấy đầu ra như sau:
```
> Ready!
> API: http://127.0.0.1:2024
> Docs: http://127.0.0.1:2024/docs
> LangGraph Studio Web UI: https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024
```

Truy cập **LangGraph Studio Web UI** qua URL trên.

Tại tab `configuration`:
- Chọn công cụ tìm kiếm web (`Tavily` hoặc `Perplexity`).
- Đặt tên mô hình LLM để sử dụng qua **Groq API**.
- Định cấu hình độ sâu vòng lặp nghiên cứu (mặc định là `3`).

## 📤 Outputs

- **Kết quả nghiên cứu:** Được lưu dưới dạng tệp markdown có trích dẫn nguồn.
- **Dữ liệu thu thập được:** Lưu trữ trong trạng thái đồ thị của LangGraph Studio.

## 🚀 Các tùy chọn triển khai

Có nhiều cách triển khai LangGraph. Xem tài liệu chi tiết tại [Module 6](https://github.com/langchain-ai/langchain-academy/tree/main/module-6) của LangChain Academy.

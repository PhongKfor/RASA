
## Hướng Dẫn Cài Đặt và Sử Dụng Rasa

Dưới đây là hướng dẫn đầy đủ để **cài đặt và sử dụng Rasa** trên máy tính của bạn. Hướng dẫn này sẽ bao gồm cách cài đặt môi trường ảo, cài đặt Rasa, và tạo một dự án cơ bản với Rasa.

---

## 1. Cài đặt môi trường ảo (Virtual Environment)

Trước khi cài đặt Rasa, bạn nên tạo một môi trường ảo để giữ cho các thư viện không xung đột với hệ thống Python hiện tại.

### Tạo môi trường ảo:
1. **Cài đặt Python (3.8-3.9) nếu chưa có.**  
   Đảm bảo Python đã được cài đặt và phiên bản của bạn là 3.8 trở lên (khuyến nghị 3.9).
   
   Kiểm tra phiên bản Python:
   ```bash
   python --version
   ```

2. **Tạo môi trường ảo**:
   Mở terminal hoặc Command Prompt và chạy lệnh sau:
   ```bash
   python -m venv .\venv
   ```

3. **Kích hoạt môi trường ảo**:
   - **Windows**:
     ```bash
     .\venv\scripts\activate
     ```
   - **Linux/MacOS**:
     ```bash
     source venv/bin/activate
     ```

Sau khi kích hoạt môi trường ảo, bạn sẽ thấy tên môi trường ảo xuất hiện trong dấu nhắc lệnh (ví dụ: `(venv)`).

---

## 2. Cài đặt Rasa

### Cài đặt Rasa đầy đủ (bao gồm tất cả các phụ thuộc và học máy):
1. **Cài đặt Rasa bằng pip**:
   Trong môi trường ảo, chạy lệnh sau để cài đặt Rasa:
   ```bash
   pip install rasa
   ```

   **Lưu ý:** Bạn có thể cài đặt Rasa với các phụ thuộc học máy (như **TensorFlow** hoặc **PyTorch**) bằng lệnh sau:
   ```bash
   pip install rasa[full]
   ```

   Tuy nhiên, nếu không cần các thư viện học máy phức tạp, bạn có thể chỉ cài đặt Rasa cơ bản mà không cần các mô-đun học máy nặng:
   ```bash
   pip install rasa
   ```

---

## 3. Tạo Dự Án Rasa

### Tạo một dự án Rasa mới:
Sau khi cài đặt Rasa, bạn có thể tạo một dự án Rasa mới với lệnh sau:
```bash
rasa init
```

Lệnh này sẽ tạo ra một thư mục dự án với cấu trúc cơ bản, bao gồm:
- **data/**: Chứa các tệp dữ liệu huấn luyện (câu hỏi và trả lời, các intents, etc).
- **actions.py**: Tệp chứa logic của các action tùy chỉnh.
- **config.yml**: Cấu hình của pipeline xử lý ngôn ngữ tự nhiên.
- **domain.yml**: Các thông tin về intents, entities, actions và responses.

Lệnh `rasa init` cũng sẽ cung cấp một mẫu chatbot đơn giản mà bạn có thể thử nghiệm ngay.

---

## 4. Huấn luyện mô hình

Sau khi dự án được tạo ra, bạn có thể huấn luyện mô hình Rasa với dữ liệu mẫu đã có.

Chạy lệnh sau để huấn luyện mô hình:
```bash
rasa train
```

Rasa sẽ sử dụng các tệp dữ liệu trong thư mục **data/** để huấn luyện mô hình và lưu mô hình đã huấn luyện vào thư mục **models/**.

---

## 5. Chạy Server và Chatbot

### Chạy chatbot trong chế độ shell:
Sau khi huấn luyện xong, bạn có thể chạy chatbot trong chế độ shell để thử nghiệm:
```bash
rasa shell
```
Điều này sẽ khởi động một môi trường dòng lệnh nơi bạn có thể trò chuyện với bot. Bạn có thể nhập các câu hỏi, và Rasa sẽ phản hồi dựa trên mô hình huấn luyện.

### Chạy server Rasa (HTTP API):
Nếu bạn muốn tương tác với chatbot qua HTTP, bạn có thể chạy server Rasa với lệnh:
```bash
rasa run
```
Điều này sẽ khởi động một API HTTP mà bạn có thể gửi yêu cầu đến (ví dụ, qua cURL, Postman, hoặc tích hợp vào ứng dụng web của bạn).

---

## 6. Cập nhật và triển khai chatbot

Khi bạn muốn cập nhật chatbot, bạn có thể:

1. **Chỉnh sửa tệp dữ liệu huấn luyện** trong thư mục **data/** (thêm intents, entities, stories).
2. **Huấn luyện lại mô hình** bằng cách chạy lại `rasa train`.
3. **Kiểm tra lại** chatbot với `rasa shell` hoặc triển khai lại lên server.

---

## 7. Các câu lệnh hữu ích khác

- **Xem trạng thái của mô hình**:
   ```bash
   rasa status
   ```
   
- **Kiểm tra dữ liệu huấn luyện** (kiểm tra dữ liệu trước khi huấn luyện):
   ```bash
   rasa data validate
   ```

- **Chạy và thử nghiệm với các hành động tùy chỉnh**:
   Nếu bạn muốn thử nghiệm với các hành động tùy chỉnh trong dự án Rasa của mình, bạn có thể tạo các action trong tệp **actions.py** và chạy chúng bằng cách sử dụng lệnh:
   ```bash
   rasa run actions
   ```

---

## Tóm lại

- Tạo môi trường ảo và kích hoạt nó.
- Cài đặt Rasa bằng `pip install rasa`.
- Sử dụng lệnh `rasa init` để tạo dự án mới.
- Huấn luyện mô hình với `rasa train`.
- Thử nghiệm chatbot với `rasa shell` hoặc chạy server với `rasa run`.

---
[Cấu trúc của 1 dự án rasa cơ bản](rasa_project_structure.md)

[Hướng dẫn tạo chatbot tư vấn tuyển sinh](TrainRasa.md)

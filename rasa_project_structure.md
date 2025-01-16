# Hướng dẫn Cấu Trúc Dự Án Rasa

Dưới đây là hướng dẫn chi tiết về cấu trúc các tệp và thư mục trong một dự án Rasa, giải thích vai trò của từng thành phần như `actions`, `data`, `models`, và các tệp cấu hình quan trọng.

## 1. Thư mục `actions`
Chứa các tệp Python định nghĩa các hành động tùy chỉnh mà bot có thể thực hiện.

- **`__pycache__`**: Thư mục lưu trữ các file bytecode (.pyc) được biên dịch tự động từ các script Python trong thư mục `actions`.
- **`__init__.py`**: File giúp Python nhận diện thư mục này như là một module. File này có thể để trống hoặc chứa mã.
- **`actions.py`**: File chính chứa các hàm định nghĩa các hành động tùy chỉnh cho bot, chẳng hạn như gọi API hoặc thực hiện các phép tính.

## 2. Thư mục `data`
Chứa dữ liệu đào tạo và các quy tắc cho bot.

- **`nlu.yml`**: Chứa các intent (ý định), entities (thực thể) và các câu ví dụ mà người dùng có thể nhập vào.
- **`rules.yml`**: Định nghĩa các quy tắc xử lý hội thoại trong các tình huống cụ thể.
- **`stories.yml`**: Chứa các kịch bản hội thoại mẫu để bot học cách phản hồi phù hợp.

## 3. Thư mục `models`
Lưu trữ các mô hình đã được đào tạo của Rasa. Mô hình này được tạo ra sau khi chạy lệnh `rasa train` và được sử dụng trong quá trình bot hoạt động để dự đoán intent và hành động.

## 4. Thư mục `tests`
Chứa các bài kiểm tra kịch bản hội thoại để đảm bảo bot hoạt động đúng như mong đợi. Các bài test này thường được sử dụng để kiểm tra tính ổn định và độ chính xác của bot.

## 5. Thư mục `venv`
Môi trường ảo Python của dự án, nơi lưu trữ các thư viện và gói cần thiết để tránh ảnh hưởng đến các dự án khác trên cùng hệ thống.

## 6. File `config.yml`
File cấu hình chính của Rasa, bao gồm:

- **Pipeline**: Quy trình xử lý ngôn ngữ tự nhiên (NLU).
- **Policies**: Chính sách điều hướng hội thoại.
- Các thành phần khác phục vụ quá trình hoạt động của bot.

## 7. File `credentials.yml`
File chứa thông tin đăng nhập cho các dịch vụ bên ngoài như Telegram, Facebook Messenger, hoặc các kênh giao tiếp khác.

## 8. File `domain.yml`
File định nghĩa domain của bot, bao gồm:

- **Intents**: Ý định của người dùng.
- **Entities**: Thực thể được trích xuất từ văn bản.
- **Slots**: Dữ liệu được lưu tạm thời trong hội thoại.
- **Responses**: Phản hồi mà bot sẽ gửi.
- **Actions**: Các hành động bot có thể thực hiện.

## 9. File `endpoints.yml`
Cấu hình các điểm cuối cho:

- **Action Server**: Thực hiện các hành động tùy chỉnh.
- **Tracker Store**: Lưu trạng thái hội thoại.
- Các kênh giao tiếp khác.

---
Mỗi thành phần trên đều có vai trò quan trọng, giúp bot hoạt động mượt mà và dễ dàng tùy chỉnh theo yêu cầu của người dùng.

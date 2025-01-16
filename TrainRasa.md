# Hướng dẫn tạo chatbot tư vấn tuyển sinh với Rasa

Dưới đây là hướng dẫn tạo một chatbot tư vấn tuyển sinh cho KMA bằng Rasa, bao gồm các tệp cấu hình như `nlu.yml`, `rules.yml`, `stories.yml`, và `domain.yml`.

## 1. Cấu hình tệp `nlu.yml`

Tệp `nlu.yml` dùng để huấn luyện Rasa nhận diện các **intent** (ý định) và **entities** (thực thể) từ dữ liệu đầu vào của người dùng. Dưới đây là ví dụ về các câu hỏi mà người dùng có thể hỏi về tuyển sinh KMA.

#### Ví dụ về tệp `nlu.yml`:

```yaml
version: "3.1"
nlu:
  - intent: ask_program
    examples: |
      - KMA có chương trình đào tạo nào?
      - Các ngành học tại KMA là gì?
      - KMA có các chương trình đào tạo cử nhân và thạc sĩ không?
      - Chương trình học của KMA bao gồm những gì?

  - intent: ask_admission
    examples: |
      - Làm thế nào để đăng ký vào KMA?
      - KMA yêu cầu gì khi nộp hồ sơ?
      - Tôi cần làm gì để đăng ký tuyển sinh KMA?
      - Khi nào tôi có thể đăng ký?

  - intent: ask_criteria
    examples: |
      - KMA có yêu cầu gì về điểm số để nhập học không?
      - Điều kiện xét tuyển vào KMA là gì?
      - Có cần thi đầu vào không?
      - KMA yêu cầu trình độ học vấn như thế nào?

  - intent: ask_deadline
    examples: |
      - Hạn cuối để nộp hồ sơ là khi nào?
      - Khi nào là ngày cuối cùng để nộp đơn?
      - KMA có hạn nộp hồ sơ không?

  - intent: greet
    examples: |
      - Xin chào
      - Chào bạn
      - Hi

  - intent: goodbye
    examples: |
      - Tạm biệt
      - Hẹn gặp lại
      - Chào nhé
```

## 2. Cấu hình tệp `rules.yml`

Tệp `rules.yml` xác định các quy tắc đối thoại (rules) để chatbot có thể phản hồi một cách chính xác khi người dùng hỏi các câu hỏi khác nhau.

#### Ví dụ về tệp `rules.yml`:

```yaml
version: "3.1"
rules:
  - rule: Greet and ask for help
    steps:
      - intent: greet
      - action: utter_greet
      - action: utter_ask_help

  - rule: Farewell
    steps:
      - intent: goodbye
      - action: utter_goodbye

  - rule: Ask about programs
    steps:
      - intent: ask_program
      - action: utter_program_info

  - rule: Ask about admission
    steps:
      - intent: ask_admission
      - action: utter_admission_info

  - rule: Ask about criteria
    steps:
      - intent: ask_criteria
      - action: utter_criteria_info

  - rule: Ask about deadline
    steps:
      - intent: ask_deadline
      - action: utter_deadline_info
```

## 3. Cấu hình tệp `stories.yml`

Tệp `stories.yml` giúp Rasa học cách quản lý cuộc trò chuyện. Bạn sẽ cung cấp các câu chuyện (stories), mô tả các tình huống mà chatbot có thể gặp phải và hành động mà nó cần thực hiện.

#### Ví dụ về tệp `stories.yml`:

```yaml
version: "3.1"
stories:
  - story: User asks for program information
    steps:
      - intent: ask_program
      - action: utter_program_info

  - story: User asks for admission information
    steps:
      - intent: ask_admission
      - action: utter_admission_info

  - story: User asks for entrance criteria
    steps:
      - intent: ask_criteria
      - action: utter_criteria_info

  - story: User asks for application deadline
    steps:
      - intent: ask_deadline
      - action: utter_deadline_info
```

Mỗi câu chuyện mô tả một chuỗi các bước trong cuộc trò chuyện. Ví dụ, khi người dùng hỏi về chương trình (intent: ask_program), chatbot sẽ trả lời với thông tin về chương trình (action: utter_program_info).

## 4. Cấu hình tệp `domain.yml`

Tệp `domain.yml` định nghĩa các thành phần cần thiết cho chatbot, bao gồm intents, responses, và actions. Đây là nơi bạn định nghĩa các câu trả lời mà chatbot có thể sử dụng.

#### Ví dụ về tệp `domain.yml`:

```yaml
version: "3.1"
intents:
  - ask_program
  - ask_admission
  - ask_criteria
  - ask_deadline
  - greet
  - goodbye

responses:
  utter_greet:
    - text: "Chào bạn! Tôi có thể giúp gì cho bạn về quy trình tuyển sinh của KMA?"
  
  utter_ask_help:
    - text: "Bạn có thể hỏi tôi bất kỳ câu hỏi nào về các chương trình, yêu cầu đầu vào hay thời gian tuyển sinh."

  utter_goodbye:
    - text: "Tạm biệt! Chúc bạn một ngày tốt lành!"

  utter_program_info:
    - text: "KMA có các chương trình đào tạo cử nhân và thạc sĩ, bao gồm các ngành như công nghệ thông tin, quản trị kinh doanh và nhiều ngành khác."

  utter_admission_info:
    - text: "Để đăng ký vào KMA, bạn cần điền đơn đăng ký trực tuyến và nộp bảng điểm học tập. Hạn chót nộp hồ sơ là ngày 30 tháng 6."

  utter_criteria_info:
    - text: "Yêu cầu đầu vào của KMA bao gồm bằng tốt nghiệp trung học và phải vượt qua kỳ thi tuyển sinh. Ngoài ra, bạn cần có điểm trung bình tối thiểu là 3.0."

  utter_deadline_info:
    - text: "Hạn chót để nộp hồ sơ tuyển sinh vào KMA là ngày 30 tháng 6. Hãy chắc chắn rằng bạn đã nộp đầy đủ các tài liệu cần thiết trước ngày này."
```

## Các bước thực hiện:

1. **Tạo các tệp dữ liệu cơ bản**:

   - Tạo các tệp `nlu.yml`, `rules.yml`, `stories.yml`, và `domain.yml` trong thư mục `data/` của dự án Rasa của bạn.

2. **Huấn luyện mô hình Rasa**:

   Sau khi tạo các tệp dữ liệu trên, bạn có thể huấn luyện mô hình bằng cách chạy lệnh:

   ```bash
   rasa train
   ```

3. **Kiểm tra mô hình với rasa shell**:

   Sau khi huấn luyện, bạn có thể kiểm tra chatbot với lệnh:

   ```bash
   rasa shell
   ```

4. **Tùy chỉnh thêm**:

   Bạn có thể tiếp tục thêm các intent, entities, và action tùy chỉnh vào các tệp cấu hình khi cần thiết.

## Tóm tắt:

- **nlu.yml**: Cung cấp dữ liệu huấn luyện cho Rasa để nhận diện các intent và entities.
- **rules.yml**: Xác định các quy tắc đối thoại mà chatbot sẽ làm theo.
- **stories.yml**: Cung cấp các câu chuyện để Rasa học cách quản lý cuộc trò chuyện.
- **domain.yml**: Định nghĩa các intents, responses, và actions trong hệ thống.

Bạn có thể sử dụng cấu hình này làm cơ sở cho chatbot tư vấn tuyển sinh của KMA. Sau khi có các tệp cấu hình, hãy huấn luyện lại mô hình và kiểm tra kết quả.

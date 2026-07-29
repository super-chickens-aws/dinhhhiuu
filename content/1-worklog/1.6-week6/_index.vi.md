+++
title = "1.6 Tuần 6 - Xây dựng chức năng Text-to-Speech"
weight = 6

[params]
  collapsibleMenu = true
+++

## Mục tiêu

Trong tuần thứ sáu, tôi tập trung phát triển chức năng chính của dự án là chuyển đổi văn bản thành giọng nói (Text-to-Speech). Mục tiêu là tích hợp dịch vụ Amazon Polly vào hệ thống Backend Serverless, xây dựng API xử lý yêu cầu từ người dùng và trả về kết quả là tệp âm thanh được tổng hợp bằng trí tuệ nhân tạo.

---

## 6.1 Tìm hiểu Amazon Polly

Trước khi bắt đầu phát triển chức năng, tôi tìm hiểu dịch vụ Amazon Polly.

Amazon Polly là dịch vụ AI của AWS có khả năng chuyển đổi văn bản thành giọng nói tự nhiên bằng công nghệ tổng hợp giọng nói (Text-to-Speech).

Trong quá trình tìm hiểu, tôi nghiên cứu các nội dung:

- Các ngôn ngữ được hỗ trợ.
- Các giọng đọc (Voice).
- Các Engine tổng hợp giọng nói.
- Các định dạng âm thanh đầu ra.
- Các API do AWS SDK cung cấp.

Qua đó, tôi hiểu được quy trình Amazon Polly tiếp nhận văn bản, xử lý và sinh ra dữ liệu âm thanh.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog48.jpg)

---

## 6.2 Thiết kế chức năng Text-to-Speech

Sau khi tìm hiểu Amazon Polly, tôi tiến hành thiết kế chức năng Text-to-Speech cho dự án.

Luồng xử lý được xây dựng như sau:

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog49.png)


Với kiến trúc này, toàn bộ quá trình xử lý được thực hiện trên nền tảng Serverless.

---

## 6.3 Cấu hình quyền truy cập Amazon Polly

Để AWS Lambda có thể gọi Amazon Polly, tôi tiến hành cấu hình IAM Role.

Các bước thực hiện: **IAM → Roles**

Sau đó cấp quyền: **AmazonPollyFullAccess**

hoặc Policy chỉ cho phép: **polly:SynthesizeSpeech**

Sau khi hoàn thành, Lambda đã có quyền sử dụng Amazon Polly.

---

## 6.4 Tích hợp AWS SDK vào Lambda

Sau khi tìm hiểu Amazon Polly, tôi tiến hành tích hợp **AWS SDK** vào hàm AWS Lambda để có thể gửi yêu cầu tổng hợp giọng nói.

Đầu tiên, tôi cài đặt thư viện AWS SDK cho Amazon Polly:

```bash
npm install @aws-sdk/client-polly
```

Tiếp theo, tôi khởi tạo **Polly Client** và cấu hình Region sử dụng:

```javascript
import { PollyClient } from "@aws-sdk/client-polly";

const client = new PollyClient({
    region: "ap-southeast-1"
});
```

Sau khi khởi tạo thành công, tôi tạo yêu cầu gửi tới Amazon Polly:

```javascript
import {
    PollyClient,
    SynthesizeSpeechCommand
} from "@aws-sdk/client-polly";

const client = new PollyClient({
    region: "ap-southeast-1"
});

const command = new SynthesizeSpeechCommand({
    Text: "Hello AWS",
    OutputFormat: "mp3",
    VoiceId: "Joanna"
});

const response = await client.send(command);
```

Trong đó:

| Thành phần | Chức năng |
|------------|-----------|
| `Text` | Nội dung văn bản cần chuyển thành giọng nói |
| `OutputFormat` | Định dạng tệp âm thanh trả về |
| `VoiceId` | Giọng đọc được sử dụng |
| `client.send()` | Gửi yêu cầu tới dịch vụ Amazon Polly |

Thông qua nội dung này, tôi hiểu cách sử dụng AWS SDK để giao tiếp với Amazon Polly và chuẩn bị cho việc xây dựng chức năng Text-to-Speech ở các bước tiếp theo.

---

## 6.5 Xây dựng API Text-to-Speech

Sau khi hoàn thành việc kết nối với Amazon Polly, tôi tiến hành xây dựng API **Text-to-Speech** để chuyển văn bản thành giọng nói.

API nhận yêu cầu từ Frontend dưới dạng JSON.

Ví dụ dữ liệu gửi lên:

```json
{
    "text": "Xin chào AWS",
    "voice": "Linh",
    "engine": "neural"
}
```

Sau khi nhận yêu cầu, Lambda thực hiện các bước:

1. Đọc dữ liệu từ Request.
2. Kiểm tra nội dung văn bản.
3. Gửi yêu cầu tới Amazon Polly.
4. Nhận kết quả âm thanh.
5. Trả kết quả về cho Frontend.

Ví dụ mã nguồn:

```javascript
import {
    PollyClient,
    SynthesizeSpeechCommand
} from "@aws-sdk/client-polly";

const client = new PollyClient({
    region: "ap-southeast-1"
});

export const handler = async (event) => {
    const { text, voice, engine } = JSON.parse(event.body);

    const command = new SynthesizeSpeechCommand({
        Text: text,
        VoiceId: voice,
        Engine: engine,
        OutputFormat: "mp3"
    });

    const response = await client.send(command);

    return {
        statusCode: 200,
        body: JSON.stringify({
            message: "Text-to-Speech thành công"
        })
    };
};
```

Đoạn mã trên minh họa quy trình xử lý cơ bản của API. Trong dự án thực tế, sau khi Amazon Polly tổng hợp giọng nói, dữ liệu âm thanh sẽ được xử lý và gửi về cho ứng dụng Frontend để người dùng có thể phát hoặc tải xuống.

Thông qua quá trình này, tôi hiểu được cách xây dựng một API Serverless trên AWS Lambda và tích hợp với Amazon Polly để cung cấp chức năng chuyển văn bản thành giọng nói.

---

## 6.6 Thiết lập các tham số tổng hợp giọng nói

Sau khi xây dựng API Text-to-Speech, tôi tiếp tục nghiên cứu các tham số mà Amazon Polly cung cấp để tùy chỉnh giọng nói đầu ra.

Các tham số chính được sử dụng gồm:

| Tham số | Mô tả |
|----------|------|
| **VoiceId** | Xác định giọng đọc sẽ sử dụng, ví dụ: `Joanna`, `Matthew`,... |
| **Engine** | Chọn công nghệ tổng hợp giọng nói, như `standard`, `neural` hoặc `generative` (nếu được hỗ trợ). |
| **OutputFormat** | Định dạng tệp âm thanh trả về, phổ biến là `mp3`, `ogg_vorbis` và `pcm`. |
| **LanguageCode** | Ngôn ngữ của giọng đọc. Một số Voice sẽ tự xác định ngôn ngữ nên không bắt buộc phải khai báo. |

Ví dụ cấu hình khi gửi yêu cầu đến Amazon Polly:

```javascript
const command = new SynthesizeSpeechCommand({
    Text: "Xin chào AWS",
    VoiceId: "Matthew",
    Engine: "neural",
    OutputFormat: "mp3"
});
```

Trong quá trình thực hành, tôi thử nghiệm nhiều giọng đọc và nhận thấy mỗi Voice có đặc điểm phát âm, ngữ điệu và ngôn ngữ hỗ trợ khác nhau. Đối với tiếng Việt, tôi sử dụng **VoiceId `Matthew`** kết hợp với **Engine `neural`** để tạo ra chất lượng âm thanh tự nhiên và rõ ràng hơn.

Thông qua việc cấu hình các tham số trên, tôi hiểu cách tùy chỉnh giọng nói đầu ra để đáp ứng các nhu cầu khác nhau của người dùng, đồng thời lựa chọn được cấu hình phù hợp cho ứng dụng Text-to-Speech.

---

## 6.7 Xử lý dữ liệu âm thanh

Sau khi Amazon Polly tổng hợp giọng nói, Lambda nhận về dữ liệu âm thanh dưới dạng luồng dữ liệu (Audio Stream).

Tôi thực hiện:

- Chuyển đổi dữ liệu về định dạng phù hợp.
- Thiết lập Content-Type.
- Trả dữ liệu về Frontend thông qua API Gateway.

Sau khi hoàn thành, Frontend có thể phát trực tiếp hoặc tải xuống tệp âm thanh.

---

## 6.8 Kiểm thử chức năng

Sau khi hoàn thành chức năng, tôi tiến hành kiểm thử.

Các nội dung kiểm thử gồm:

- Văn bản ngắn.
- Văn bản dài.
- Nội dung tiếng Việt.
- Nội dung tiếng Anh.
- Nhiều Voice khác nhau.
- Các Engine khác nhau.

Ngoài ra, tôi kiểm tra các trường hợp:

- Văn bản rỗng.
- Văn bản vượt quá giới hạn.
- Voice không tồn tại.

Kết quả cho thấy API hoạt động đúng theo yêu cầu thiết kế.

---

## 6.9 Tối ưu xử lý

Sau khi chức năng hoạt động ổn định, tôi tiến hành tối ưu mã nguồn.

Các nội dung thực hiện:

- Chuẩn hóa cấu trúc mã nguồn.
- Tách Business Logic khỏi Handler.
- Bổ sung xử lý ngoại lệ.
- Chuẩn hóa định dạng Response.
- Bổ sung ghi log phục vụ kiểm thử.

Việc tối ưu giúp mã nguồn dễ bảo trì và thuận tiện cho việc mở rộng các chức năng trong tương lai.

---

## 6.10 Khó khăn gặp phải

Trong quá trình tích hợp Amazon Polly, tôi gặp một số khó khăn khi xử lý dữ liệu âm thanh trả về từ dịch vụ cũng như việc cấu hình quyền truy cập giữa AWS Lambda và Amazon Polly.

Bên cạnh đó, việc xử lý các trường hợp dữ liệu đầu vào không hợp lệ và đảm bảo API luôn trả về kết quả đúng định dạng cũng cần được kiểm tra cẩn thận.

---

## 6.11 Cách giải quyết

Để giải quyết các vấn đề trên, tôi tham khảo tài liệu chính thức của AWS, kiểm tra log trên CloudWatch và thực hiện nhiều lần kiểm thử với các loại dữ liệu đầu vào khác nhau.

Ngoài ra, tôi tách riêng phần xử lý nghiệp vụ khỏi phần tiếp nhận yêu cầu của Lambda, giúp mã nguồn rõ ràng hơn và thuận tiện trong quá trình bảo trì.

---

## 6.12 Kiến thức đạt được

Sau tuần thứ sáu, tôi đã:

- Hiểu nguyên lý hoạt động của Amazon Polly.
- Biết cách sử dụng AWS SDK để gọi dịch vụ AWS.
- Tích hợp thành công Amazon Polly với AWS Lambda.
- Xây dựng API chuyển văn bản thành giọng nói.
- Biết cách xử lý dữ liệu âm thanh trả về từ Amazon Polly.
- Hiểu luồng xử lý giữa Frontend, API Gateway, Lambda và Amazon Polly.
- Hoàn thiện chức năng cốt lõi của dự án.

---

## 6.13 Đánh giá của bản thân

Tuần thứ sáu là giai đoạn quan trọng nhất trong quá trình phát triển dự án vì chức năng chính của ứng dụng đã được hoàn thiện. Việc tích hợp thành công Amazon Polly với kiến trúc Serverless giúp tôi hiểu rõ hơn cách kết hợp các dịch vụ AI của AWS để xây dựng ứng dụng thực tế.

Sau khi hoàn thành tuần này, hệ thống đã có khả năng tiếp nhận văn bản từ người dùng, chuyển đổi thành giọng nói và trả kết quả thông qua API. Đây là nền tảng để trong tuần tiếp theo tôi tiếp tục xây dựng giao diện người dùng, tích hợp Frontend với Backend và triển khai ứng dụng lên Internet bằng AWS Amplify.
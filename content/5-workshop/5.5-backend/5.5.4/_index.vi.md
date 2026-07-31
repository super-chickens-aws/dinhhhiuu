+++
title = '5.5.4 Api Gateway'
weight = 4

[params]
  collapsibleMenu = true
+++

## Thiết lập cổng giao tiếp

Truy cập **API Gateway** → **Create API**.

Chọn **HTTP API** → **Build**.

API name: `polly-voice`

Integrations -> Lambda -> polly-voice

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj5.png)

Thiết lập các tuyến đường phù hợp.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj6.png)

Xác định các giai đoạn.

> Không thay đổi gì.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj7.png)

Nhấn **Create** để hoàn thành.

---

## Kiểm tra lại

Truy cập: **API Gateway** → **APIs** → **[name]-api ([id]-api)** → **Stages**

Lúc này sẽ có đường dẫn (URL) để kiểm tra API.

---

## Thiết lập Authorization

Truy cập: **API Gateway** → **APIs** → **Routes - [tên api] ([id api])** → **Authorization**

Chọn **Create and attach authorizer**.

Thiết lập các thông số sau:

- **Authorizer type:** `JWT`
- **Identity Source:** Giữ mặc định `$request.header.Authorization`
- **Issuer:** `https://cognito-idp.ap-southeast-1.amazonaws.com/ap-southeast-1_xxxxxxx`
- **Audience:** `App Client ID (3l8g0j7vxxxxxxxxxxxx)`
- **Name:** `polly-voice-auth`

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj9.png)

Nhấn **Save** để hoàn thành.

> **Lưu ý**
>
> Với `$request.header.Authorization`, API Gateway sẽ đọc giá trị từ header:
>
> ```text
> Authorization: Bearer xxxxxxxxx
> ```

```text
Issuer: Cognito → User Pool → Overview → User Pool ID

Ví dụ:

Region: ap-southeast-1
User Pool ID: ap-southeast-1_abcd123

Issuer sẽ là:
https://cognito-idp.ap-southeast-1.amazonaws.com/ap-southeast-1_abcd123
```

Sau đó nhấn **Attach authorizer** để hoàn thành.

---

## Thiết lập CORS

Truy cập: **API Gateway** → **APIs** → **[name-api] ([id-api])** → **CORS**

Thiết lập các thông số:

- **Access-Control-Allow-Origin:** Đường dẫn frontend được phép truy cập.
- **Access-Control-Allow-Methods:** Các phương thức được phép sử dụng.
- **Access-Control-Allow-Headers:** Các header được phép gửi.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj10.png)

Nhấn **Save** để hoàn thành.
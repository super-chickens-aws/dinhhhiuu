+++
title = '5.6 Xây dựng Frontend'
weight = 6

[params]
  collapsibleMenu = true
+++

## Đưa website lên Internet

Clone mã nguồn tại đây và tạo repo mới:

**GitHub Repository**

https://github.com/super-chickens-aws/polly-voice

Truy cập **AWS Amplify** → **Deploy an app**.

Tại mục **To deploy an app from a Git provider**, chọn **GitHub**.

Thực hiện các bước sau:

1. Chọn **repository GitHub** cần xây dựng.
2. Chọn **branch**.
3. Chọn **folder** nếu dự án là **Monorepo**.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj11.png)

Tiếp theo, cấu hình ứng dụng:

- **App name:** `polly-voice`
- **Build command:** `npm run build`
- **Build output directory:** `dist`

Sau khi hoàn tất, nhấn **Save and deploy** để bắt đầu triển khai ứng dụng.

---

## Thêm biến môi trường

Truy cập: **AWS Amplify** → **Environment Variables** → **Manage variables**

Thêm các biến môi trường cần thiết.

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj12.png)

Sau khi thêm đầy đủ các biến môi trường, nhấn **Save** để lưu cấu hình.
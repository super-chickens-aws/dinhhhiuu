+++
title = '5.5 DynamoDB'
weight = 5

[params]
  collapsibleMenu = true
+++

## Tạo bảng DynamoDB lưu thông tin user

DynamoDB -> Create table

Thiết lập tên bảng và khóa partition phù hợp

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj13.png)

## Cấp quyền cho Lambda

Hiện lambda chưa có quyền truy cập DynamoDB nên chúng ta phải dùng IAM Role để cấp

Lambda -> Function -> voice-ai-api -> Configuration -> Permissions

Execution role -> Role name

Trong IAM -> Add permissions -> Create inline policy

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj14.png)

Actions cấp 3 quyền: GetItem, PutItem, UpdateItem

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj15.png)

Đặt tên cho policy

Ấn **Create** để hoàn thành
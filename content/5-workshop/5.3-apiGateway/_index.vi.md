+++
title = '5.3 Api Gateway'
weight = 3

[params]
  collapsibleMenu = true
+++

## Thiết lập cổng giao tiếp 

API Gateway -> Create API

Chọn **HTTP API** -> **Build**

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj5.png)

Thiết lập các tuyến đường phù hợp

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj6.png)

Xác định các giai đoạn

không thay đổi gì

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj7.png)

Ấn `Create` để hoàn thành

## Kiểm tra lại 
API Gateway -> APIs -> [name]-api ([id]-api) -> Stages

Lúc này sẽ có link để kiểm tra

## Tạo route
API Gateway -> APIs -> Routes - [tên api](id api) -> Create a route

Thiết lập phương thức và end point

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj8.png)

Ấn **Create** để hoàn thành

## Thiết lập Authorization

API Gateway -> APIs -> Routes - [tên api](id api) -> Authorization

Chọn Create and attach authorizer

- Authorizer type: JWT
- Identity Source: Để mặc định $request.header.Authorization
- Issuer: https://cognito-idp.ap-southeast-1.amazonaws.com/ap-southeast-1_xxxxxxx
- Audience: App Client ID (3l8g0j7vxxxxxxxxxxxx)
- Tên: Tự đặt

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj9.png)

Ấn **Save** để hoàn thành

`Với $request.header.Authorization: API Gateway sẽ đọc Authorization: Bearer xxxxxxxxx`
```text
Issuer: Cognito -> User Pool -> Overview -> User Pool ID. 

Ví dụ: 
Region: ap-southeast-1
UserPool: ap-southeast-1_abcd123

Issuer sẽ là: https://cognito-idp.ap-southeast-1.amazonaws.com/ap-southeast-1_abcd123
```

Ấn **Attach authorizer** để hoàn thành

## Thiết lập CORS

API Gateway -> APIs -> [name-api](id-api) -> CORS

- Access-Control-Allow-Origin: Link frontend được phép truy cập
- Access-Control-Allow-Methods: Các phương thức được sử dụng 
- Access-Control-Allow-Headers: Các nội dung được phép  

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj10.png)

Ấn **Save** để hoàn thành
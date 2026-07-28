+++
title = '5.6 S3 và Polly'
weight = 3

[params]
  collapsibleMenu = true
+++

## Tạo S3 để lưu

Amazon S3
Buckets
Create bucket

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj16.png)

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj17.png)

Mở bucket
Create folder

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj18.png)

Lưu lại Bucketname: **voice-ai-media-superchicken**

## Gán quyền để lambda truy cập và sử dụng được S3 và Polly

Lambda
Configuration
Permissions
Click Role


Add permissions
Attach Policy
Tìm **AmazonPollyFullAccess**, **AmazonS3FullAccess**
Attach.

## Thiết lập để tải mp3 từ S3

S3
↓
Bucket
↓
Permissions
↓
Bucket Policy
↓
Edit

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicRead",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::voice-ai-media-superchicken/*"
    }
  ]
}
```

## Tạo bảng SpeechHistory để lưu lại text và file speech

DynamoDB
Tables
Create table

![Mô tả ảnh](https://super-chickens-aws.github.io/dinhhhiuu/images/prj19.png)

Ấn **Create** để hoàn thành

```json
{
    "userId": "abc123",
    "createdAt": "2026-07-27T16:20:10Z",
    "text": "Hello AWS",
    "voiceId": "Danielle",
    "engine": "neural",
    "speed": 100,
    "pitch": 0,
    "volume": 100,
    "audioKey": "tts/1785082534512.mp3"
}
```

## Thêm quyền truy cập Bảng SpeechHistory cho Lambda

Lambda

↓

Function

↓

Configuration

↓

Permissions

↓

Execution Role

↓

Click vào Role

Role

↓

Add permissions

↓

Create inline policy

Service

↓

DynamoDB

Resource → table → Add ARNs

Ấn **Create** 
Ấn **Next**

Đặt tên **speech-history-policy** và **Create** để hoàn thành
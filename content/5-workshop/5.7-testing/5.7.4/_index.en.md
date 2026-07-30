+++
title = '5.7.4 Test Conversion History'
weight = 4

[params]
  collapsibleMenu = true
+++

## Test Conversion History

After successfully generating and storing audio files, we should verify that the application correctly records each conversion in Amazon DynamoDB.

The conversion history allows users to review previously generated speech files without generating them again.

---

## Test Scenario

Verify the following workflow:

- Generate one or more speech files.
- Confirm that each conversion is stored in Amazon DynamoDB.
- Verify that the frontend retrieves the history correctly.
- Ensure the displayed information matches the stored data.

---

## Step 1. Generate Multiple Conversions

Log in to the Polly Voice application and generate several speech files using different input texts.

For example:

```text
Welcome to Polly Voice.

AWS Serverless makes application deployment easier.

Amazon Polly provides high-quality Text-to-Speech services.
```

Use different voices if available.

> 📷 **Screenshot:** Multiple Speech Generation Requests

---

## Step 2. Verify Records in Amazon DynamoDB

1. Open the **AWS Management Console**.
2. Navigate to **Amazon DynamoDB**.
3. Open the **PollyVoiceHistory** table.
4. Select **Explore table items**.

Verify that a new item has been created for each conversion request.

Each record should include information such as:

- User ID
- Input text
- Selected voice
- Audio URL
- Creation timestamp

> 📷 **Screenshot:** DynamoDB Table Items

---

## Step 3. Verify History on the Frontend

Return to the Polly Voice application.

Navigate to the **History** section.

Verify that all previously generated conversions are displayed correctly.

Each history item should include:

- Input text
- Voice name
- Creation time
- Audio playback option

> 📷 **Screenshot:** Conversion History Page

---

## Step 4. Verify Audio Playback from History

Select one of the previous conversion records.

Verify that:

- The audio player loads successfully.
- The correct audio file is played.
- The downloaded file matches the selected history record.

> 📷 **Screenshot:** Play Audio from History

---

## Step 5. Compare Frontend and Database

Compare the information shown on the frontend with the corresponding record stored in DynamoDB.

Verify that:

- Input text is identical.
- Voice selection is correct.
- Audio URL matches the S3 object.
- Timestamp is displayed correctly.

This confirms that the application retrieves data accurately from the database.

> 📷 **Screenshot:** Compare DynamoDB Record with Frontend

---

## Expected Result

The conversion history feature is considered successful if:

- Every speech generation request creates a new record in Amazon DynamoDB.
- The frontend retrieves the history successfully.
- All conversion information is displayed correctly.
- Users can replay previously generated audio files.
- The data displayed on the frontend matches the records stored in DynamoDB.

This confirms that Amazon DynamoDB has been successfully integrated with the Polly Voice application and can reliably store and retrieve conversion history.
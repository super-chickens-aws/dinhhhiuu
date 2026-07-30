+++
title = '5.7.3 Test Audio Storage'
weight = 3

[params]
  collapsibleMenu = true
+++

## Test Audio Storage

After the speech has been successfully generated, we should verify that the audio file is correctly stored in Amazon S3.

This test ensures that AWS Lambda uploads the generated MP3 file to the configured S3 bucket and that the file can be accessed by the frontend.

---

## Test Scenario

Verify the following workflow:

- Generate a speech file.
- Confirm that the MP3 file is uploaded to Amazon S3.
- Verify the file metadata.
- Confirm that the file can be accessed from the application.

---

## Step 1. Open the Amazon S3 Console

1. Open the **AWS Management Console**.
2. Navigate to **Amazon S3**.
3. Open the bucket created for Polly Voice.

For example:

```
polly-voice-audio
```

> 📷 **Screenshot:** Amazon S3 Bucket

---

## Step 2. Verify Uploaded Audio File

Inside the bucket, verify that a new MP3 file has been created after generating speech.

Check the following information:

- File name
- File type (.mp3)
- File size
- Upload time

The uploaded file should correspond to the most recent Text-to-Speech request.

> 📷 **Screenshot:** Generated MP3 File

---

## Step 3. Review Object Details

Select the uploaded object to view its details.

Verify that:

- The object key is correct.
- The file size is greater than zero.
- The object was uploaded successfully.
- The object is stored in the expected storage class.

> 📷 **Screenshot:** Object Details

---

## Step 4. Verify File Accessibility

Return to the Polly Voice application.

Play the generated audio using the built-in audio player.

Also verify that the **Download** button downloads the correct MP3 file from Amazon S3.

The downloaded file should match the uploaded object stored in the bucket.

> 📷 **Screenshot:** Download Generated Audio

---

## Step 5. Generate Multiple Audio Files

Repeat the Text-to-Speech process several times using different input texts.

Verify that:

- Each request creates a new MP3 file.
- Existing files are not overwritten.
- Every generated file is stored successfully in Amazon S3.

> 📷 **Screenshot:** Multiple Audio Files in S3

---

## Expected Result

The audio storage feature is considered successful if:

- Every Text-to-Speech request creates a new MP3 file.
- The generated files are stored successfully in Amazon S3.
- Object metadata is displayed correctly.
- Users can play and download the generated audio.
- Multiple requests create separate audio files without overwriting previous ones.

This confirms that Amazon S3 has been successfully integrated with the Polly Voice application and can reliably store generated speech files.
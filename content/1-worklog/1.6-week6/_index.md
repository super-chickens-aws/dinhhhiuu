+++
title = "1.6 Week 6 - Building the Text-to-Speech Feature"
weight = 6

[params]
  collapsibleMenu = true
+++

## Objectives

During the sixth week, I focused on developing the main feature of the project: converting text into speech (Text-to-Speech). The objective was to integrate Amazon Polly into the Serverless Backend, build an API to process user requests, and return AI-generated audio files.

---

## 6.1 Learning About Amazon Polly

Before developing the feature, I studied Amazon Polly.

Amazon Polly is an AWS AI service that converts text into natural-sounding speech using Text-to-Speech (TTS) technology.

During this learning process, I explored:

- Supported languages.
- Available voices.
- Speech synthesis engines.
- Output audio formats.
- APIs provided by the AWS SDK.

Through this study, I understood how Amazon Polly receives text, processes it, and generates audio data.

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog48.jpg)

---

## 6.2 Designing the Text-to-Speech Feature

After learning about Amazon Polly, I designed the Text-to-Speech feature for the project.

The processing flow was designed as follows:

![Image description](https://super-chickens-aws.github.io/dinhhhiuu/images/worklog49.png)

With this architecture, the entire processing workflow is performed on a Serverless platform.

---

## 6.3 Configuring Access Permissions for Amazon Polly

To allow AWS Lambda to call Amazon Polly, I configured the IAM Role.

Steps performed:

**IAM → Roles**

Then I granted one of the following permissions:

**AmazonPollyFullAccess**

or a policy allowing only:

**polly:SynthesizeSpeech**

After completing the configuration, the Lambda function was authorized to use Amazon Polly.

---

## 6.4 Integrating the AWS SDK into Lambda

After studying Amazon Polly, I integrated the **AWS SDK** into the AWS Lambda function so it could send speech synthesis requests.

First, I installed the AWS SDK library for Amazon Polly:

```bash
npm install @aws-sdk/client-polly
```

Next, I initialized the **Polly Client** and configured the AWS Region:

```javascript
import { PollyClient } from "@aws-sdk/client-polly";

const client = new PollyClient({
    region: "ap-southeast-1"
});
```

After initializing the client successfully, I created a request to Amazon Polly:

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

The components are described below:

| Component | Purpose |
|-----------|---------|
| `Text` | The text content to convert into speech |
| `OutputFormat` | The format of the returned audio file |
| `VoiceId` | The voice used for speech synthesis |
| `client.send()` | Sends the request to Amazon Polly |

Through this process, I learned how to use the AWS SDK to communicate with Amazon Polly and prepared for implementing the complete Text-to-Speech functionality.

---

## 6.5 Building the Text-to-Speech API

After successfully connecting to Amazon Polly, I developed the **Text-to-Speech API** to convert text into speech.

The API accepts requests from the Frontend in JSON format.

Example request payload:

```json
{
    "text": "Hello AWS",
    "voice": "Linh",
    "engine": "neural"
}
```

After receiving the request, the Lambda function performs the following steps:

1. Read the request data.
2. Validate the input text.
3. Send the request to Amazon Polly.
4. Receive the synthesized audio.
5. Return the result to the Frontend.

Example source code:

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
            message: "Text-to-Speech completed successfully"
        })
    };
};
```

The above code demonstrates the basic processing workflow of the API. In the actual project, after Amazon Polly synthesizes the speech, the audio data is processed and returned to the Frontend so users can either play or download the generated audio.

Through this implementation, I learned how to build a Serverless API using AWS Lambda and integrate it with Amazon Polly to provide Text-to-Speech functionality.

---

## 6.6 Configuring Speech Synthesis Parameters

After building the Text-to-Speech API, I continued studying the parameters provided by Amazon Polly to customize the generated speech.

The main parameters used include:

| Parameter | Description |
|-----------|-------------|
| **VoiceId** | Specifies the voice to be used, for example: `Joanna`, `Matthew`, and others. |
| **Engine** | Selects the speech synthesis technology, such as `standard`, `neural`, or `generative` (if supported). |
| **OutputFormat** | Specifies the output audio format, commonly `mp3`, `ogg_vorbis`, and `pcm`. |
| **LanguageCode** | Specifies the language of the selected voice. Some voices automatically determine the language, so this parameter is optional. |

Example configuration when sending a request to Amazon Polly:

```javascript
const command = new SynthesizeSpeechCommand({
    Text: "Hello AWS",
    VoiceId: "Matthew",
    Engine: "neural",
    OutputFormat: "mp3"
});
```

During the implementation process, I experimented with different voices and found that each voice has its own pronunciation, intonation, and supported languages. For Vietnamese text, I used **VoiceId `Matthew`** together with the **`neural` engine** to produce clearer and more natural-sounding speech.

Through configuring these parameters, I learned how to customize the generated speech to meet different user requirements and select the most suitable configuration for the Text-to-Speech application.

---

## 6.7 Processing Audio Data

After Amazon Polly synthesized the speech, AWS Lambda received the generated audio as an **Audio Stream**.

I implemented the following processing steps:

- Convert the audio stream into an appropriate format.
- Configure the correct `Content-Type` for the response.
- Return the audio data to the Frontend through Amazon API Gateway.

After completing these steps, the Frontend was able to either play the generated audio directly or allow users to download the audio file.

---

## 6.8 Testing the Text-to-Speech Function

After completing the implementation, I performed a series of tests to verify that the Text-to-Speech feature worked correctly.

The test cases included:

- Short text.
- Long text.
- Vietnamese text.
- English text.
- Different Voice options.
- Different Engine options.

I also tested several edge cases, including:

- Empty text.
- Text exceeding the supported length.
- Invalid or unsupported Voice IDs.

The testing results showed that the API functioned as expected and produced audio successfully for all valid requests.

---

## 6.9 Optimizing the Implementation

After verifying that the feature was working correctly, I optimized the source code to improve maintainability and scalability.

The optimization tasks included:

- Standardizing the project structure.
- Separating Business Logic from the Lambda Handler.
- Adding exception handling.
- Standardizing the API response format.
- Adding logging to support testing and debugging.

These improvements made the codebase cleaner, easier to maintain, and more suitable for future feature expansion.

---

## 6.10 Challenges Encountered

During the integration of Amazon Polly, I encountered several challenges related to processing the audio data returned by the service and configuring the permissions between AWS Lambda and Amazon Polly.

In addition, handling invalid user input and ensuring that the API always returned responses in the correct format required careful validation and testing.

---

## 6.11 Solutions

To resolve these issues, I referred to the official AWS documentation, reviewed execution logs in Amazon CloudWatch, and repeatedly tested the API with different input scenarios.

I also separated the business logic from the Lambda request handler, making the code easier to understand, maintain, and extend in the future.

---

## 6.12 Knowledge Gained

After completing the sixth week, I achieved the following learning outcomes:

- Understood how Amazon Polly works.
- Learned how to use the AWS SDK to communicate with AWS services.
- Successfully integrated Amazon Polly with AWS Lambda.
- Built a Serverless Text-to-Speech API.
- Learned how to process audio data returned by Amazon Polly.
- Understood the processing flow between the Frontend, Amazon API Gateway, AWS Lambda, and Amazon Polly.
- Completed the core functionality of the project.

---

## 6.13 Self-Assessment

The sixth week was the most significant stage of the project because the application's primary feature was successfully completed. Integrating Amazon Polly with a Serverless architecture gave me a deeper understanding of how AWS AI services can be combined to build practical cloud-based applications.

By the end of this week, the system was able to receive text input from users, convert it into speech, and return the generated audio through the API. This provided a solid foundation for the following week, during which I would develop the user interface, integrate the Frontend with the Backend, and deploy the complete application to the Internet using AWS Amplify.
# Using Pre-Trained Machine Learning Models

## Introduction
Pre-trained machine learning (ML) models can enhance your applications with powerful features without requiring deep ML expertise. Google Cloud offers several pre-trained ML APIs that you can use to add intelligence to your applications.

## Google Cloud ML APIs

### 1. Vision API
- **Functionality**: Performs complex image detection and analysis.
- **Features**:
  - **Label Detection**: Categorizes objects under labels.
  - **Optical Character Recognition (OCR)**: Extracts text from images.
  - **Landmark Detection**: Identifies landmarks in images.
  - **Logo Detection**: Detects logos in images.
  - **Face Detection**: Analyzes faces for emotions and headwear.
  - **Explicit Content Detection**: Identifies explicit content in images.
- **Use Case Example**:
  - **Wedding Picture**: Detects emotional expressions on faces.
  - **Sphinx Image**: Identifies the Sphinx in Las Vegas, not Egypt.

### 2. Speech-to-Text API
- **Functionality**: Converts audio to text.
- **Features**:
  - Supports 110 languages and variants.
  - Transcribes text from live audio or audio files.
  - Enables voice command-and-control for applications.
- **Use Case Example**:
  - Transcribing user dictation from a microphone.

### 3. Text-to-Speech API
- **Functionality**: Converts text to audio.
- **Features**:
  - Generates natural-sounding speech from text input.
  - Supports multiple languages and voices.

### 4. Cloud Translation API
- **Functionality**: Translates text between supported languages.
- **Features**:
  - High responsiveness for dynamic translation.
  - Translates text from a source language to a target language.
- **Use Case Example**:
  - Real-time translation for websites and applications.

### 5. Cloud Natural Language API
- **Functionality**: Extracts information from text.
- **Features**:
  - **Entity Recognition**: Identifies entities mentioned in text.
  - **Sentiment Analysis**: Understands sentiment in social media posts or customer conversations.
  - **Syntax Analysis**: Parses the structure of text.
  - **Content Classification**: Categorizes content into predefined categories.
- **Use Case Example**:
  - Understanding sentiment about products on social media.

### 6. Video Intelligence API
- **Functionality**: Searches video files to extract and label entities.
- **Features**:
  - Annotates videos at the shot, frame, or video level.
  - Identifies key entities and timestamps within videos.
- **Use Case Example**:
  - Annotating videos stored in Cloud Storage to identify when specific entities appear.

### 7. AutoML on Vertex AI
- **Functionality**: Enables users with limited ML expertise to train high-quality custom models.
- **Features**:
  - Supports training models on images, tabular data, text, or videos.
  - No code required for training models.
- **Use Case Example**:
  - Training custom ML models specific to business needs using a user-friendly interface.

### 8. Custom ML Models
- **Frameworks**: Use TensorFlow, PyTorch, and Vertex AI to build and train custom ML models.
- **Use Case Example**:
  - Developing bespoke ML models for specialized tasks using custom datasets.

## Example: Using Vision API
1. **Process an Image**:
   - Store the image in Cloud Storage.
   - Invoke the REST API with a JSON request.
   - Receive a JSON response with attributes describing the image.

2. **Example Request and Response**:
   ```json
   {
     "requests": [
       {
         "image": {
           "source": {
             "gcsImageUri": "gs://bucket_name/image.jpg"
           }
         },
         "features": [
           {
             "type": "LABEL_DETECTION"
           }
         ]
       }
     ]
   }
   ```
   **Response**:
   ```json
   {
     "labelAnnotations": [
       {
         "description": "Sphinx",
         "score": 0.95
       }
     ]
   }
   ```

## Google Use Case Example
- **Occupancy Detection**:
  - Google’s conference room systems use motion detection with VC cameras.
  - Sends Pub/Sub notifications every 30 seconds about motion detection.
  - Determines room occupancy based on motion detection within specific time frames.

## Conclusion
Pre-trained ML models from Google Cloud can add significant value to your applications by enabling advanced functionalities such as image and speech recognition, language translation, sentiment analysis, and video intelligence. These models are easy to integrate via REST APIs, making powerful ML capabilities accessible without requiring deep technical knowledge.
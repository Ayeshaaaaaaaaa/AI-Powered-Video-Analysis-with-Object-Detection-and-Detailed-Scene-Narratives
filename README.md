# AI-Powered-Video-Analysis-with-Object-Detection-and-Detailed-Scene-Narratives
AI-driven video analysis system that extracts and transcribes audio with Whisper, detects objects using YOLO, and generates comprehensive scene descriptions with GPT-2. The project combines transcriptions and object detections to produce detailed, context-aware video narratives.<br>
## Video processing & object dection using yolov8
The video is processed frame by frame.<br>
For every second (1 frame per second), a frame is extracted and passed through the YOLOv8 model.<br>
Objects detected in the frame with a confidence greater than or equal to 0.7 are stored in a list.<br>
The detections (bounding boxes, class names, and confidence scores) are saved as JSON data for each frame.<br>
The result is a detections.json file, which stores the objects detected in each frame at 1-second intervals.<br>
![image](https://github.com/user-attachments/assets/610c7f96-fbcb-43fc-b79f-ad22d2a3a949)<br>
![image](https://github.com/user-attachments/assets/6eb5faaa-2a25-4376-9537-f5a9b27f4c9a)<br>
![image](https://github.com/user-attachments/assets/c3328f94-4063-4062-a70a-d386d487d128)<br>

## Audio transcription with timestamps
**Model Transcription**: The line result = model.transcribe(audio_path, language="en", temperature=0.6, verbose=True) performs the transcription using the Whisper model:<br>
**audio_path**: Path to the audio file.<br>
**language="en"**: Specifies that the audio is in English.<br>
**temperature=0.6**: Controls the randomness of the transcription model. A higher value introduces more randomness, and a lower value makes it more deterministic. In this case, it’s set to 0.6 for a balance between creativity and accuracy.<br>
**verbose**=True: Enables detailed output during transcription<br>
It provides start and end times for each spoken segment and saves the transcription with these timestamps into a text file.<br>
The transcriptions are saved in the format: [start_time - end_time] transcribed_text.<br>
![image](https://github.com/user-attachments/assets/79b8e337-293b-43c4-9e1d-bacb5c66d1bf)<br>

## GPT-2 Model and Tokenizer Initialization:
The GPT-2 model and tokenizer are loaded from the transformers library to generate coherent text descriptions based on the given inputs.<br>
![image](https://github.com/user-attachments/assets/e6a13691-5e95-4835-ac40-63260614dd35)<br>
## Cleaning Input Text:

The function clean_input(input_text) is used to clean the detections summary and transcribed text, removing any unwanted or special characters, ensuring the input is ASCII-only.<br>
![image](https://github.com/user-attachments/assets/7e64f81c-cbe2-4d26-ae6a-2a6bc6ee9039)<br>
## Combining Detections and Transcriptions:

In the generate_description function, detections from the video and the transcribed text from the audio are combined into a formatted string (description_input), which serves as input to GPT-2 to generate the final description.<br>
![image](https://github.com/user-attachments/assets/eac054c8-74bc-4f57-b1f6-67bd6b615780)<br>
![image](https://github.com/user-attachments/assets/55762d6d-7106-4e42-a1e1-19188b8bd67f)<br>
## Processing Detections File & transcribed text:

The function process_detections_file(detections_file_path, transcribed_audio_file_path) loads the object detections (from detections.json) and transcribed text (from transcription_with_timestamps.txt), sorts them by frame, and formats the detected objects along with their bounding box positions.<br>
It then calls generate_description to generate a coherent and detailed description of the video, based on both the visual and auditory data.<br>
![image](https://github.com/user-attachments/assets/b3f867ba-e878-4fde-9331-8bfd554aafcc)<br>
![image](https://github.com/user-attachments/assets/061f0505-5b25-4402-94d5-8fbde550001b)<br>
## Output:

The final result is a natural-language description of the video, created by GPT-2, that integrates both visual elements from object detection and the context from the transcribed audio.<br>
![image](https://github.com/user-attachments/assets/169d0635-4a26-4d3a-8f44-a299964f00bf)<br>
![image](https://github.com/user-attachments/assets/dcd9f03e-97f4-42c0-b5fa-af28db312c9c)<br>
![image](https://github.com/user-attachments/assets/bf6b10a1-22d4-4b5a-8d26-c93984c296ce)<br>

## Limitations and Future Improvements:
This project currently uses the GPT-2 model to generate detailed descriptions based on object detections and transcribed audio from videos. While GPT-2 is a versatile model, it has limitations in generating coherent and contextually rich descriptions, particularly for complex tasks like video analysis. The results may not fully capture the nuances of the content due to the model’s smaller size and reduced capacity for long-range contextual understanding. To improve the quality of the generated descriptions, a more powerful model, such as GPT-3.5 or GPT-4, could be integrated. These models are better suited for handling complex tasks and generating richer, more coherent outputs. Additionally, fine-tuning on a relevant dataset or incorporating other natural language generation techniques could further enhance the results.



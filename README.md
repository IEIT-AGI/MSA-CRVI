
# Infer Induced Sentiment of Comment Response to Video: A New Task, Dataset and Baseline

 This repository aims to share and provide public CSMV datasets which is a Dataset of Infer Induced Sentiment of Comment Response to Video, offering free, open, and accessible data resources for scientists, researchers, and developers.

# Overview
The prosperity of micro video platforms has brought new topics to multimodal affective computation. The comments of a micro video convey different sentiments. Therefore, we propose a task named Multi-modal Sentiment Analysis for Comment Response of Video Induced(MSA-CRVI) to infer comment opinion and emotion with understanding the micro video. 
In light of this, we create a new dataset called Comment Sentiment toward to Micro Video (CSMV) to study this task, which includes more than 100k manually annotated comments. The key to the task is to construct the deep sentiment interaction and semantic correlation between video and comment. 
## Task
Existing multi-modal benchmarks on video include MOSI, CMU-MOSEI, and MELD. The video form in these benchmarks is monologue or dialogue. They take temporal images (e.g., facial expression, smile, and gaze), audio(e.g., tones, pauses, and voice pitch), and textual data transcribed from spoken words as a clue to infer the sentiment and emotion of the speaker.

With the development of the Internet we-media, micro video social platforms bring a new issue for multi-modal sentiment analysis. People create micro videos to showcase their individuality and express their feeling about them with comments. Unlike current benchmarks, the comments may hold different sentiments for the same micro-videos. For precise induced sentiment inference from comments, it is essential to integrate the video content. But current approaches tend to treat comment sentiment analysis to be a simple NLP task and neglect the semantic connection between videos and comments.

The CSMV dataset is collected from the most popular micro video social media platform, TikTok, which includes both the micro videos and corresponding comments.
Similar to the existing benchmark, we provide two types of annotations: opinion and emotion. The opinion labels consist of Positive, Negative, and Neutral, respectively. It indicates the comment holds agreement, disagreement, or indifferent sentiment toward the content of the videos. As for the emotion labels, we adopt the widely-used Plutchik’s wheel of emotions strategy, which includes eight labels: Trust, Joy, Surprise, Anticipation, Disgust, Sadness, Anger, and Fear.


## Video Features
### Description

For the visual feature which extracted from video frames, we present them as tensor representations which saved as npy files for each micro video. First of all, we uniform all the micro videos at same frame rate of 25fps. Afterwards, we used FFmpeg to extract all video frames. Then, we utilize the I3D model to generate the temporal features of the micro videos with a window size of 16 frames and a step size of 8. We slide the window on the temporal axis and limit the max tensor length as 180. The feature dimension is 1024.

### Download

You can download Video Features from the following location:

- Google Drive:[Video Features Download Link](https://drive.google.com/file/d/1kZUSbQsCjnx1Q4OzDiX5JAH5OExG0HxF/view?usp=sharing)
- Baidu NetDisk:[Video Features Download Link](https://pan.baidu.com/s/19K-7D4cFrY0lkhuwEVU1pg?pwd=sykw) Extract code: sykw

## Comment Annotations

### Description

For the comment data, we organize them as JSON files. We save all comments data as a json file and assign unique keys as data pointer. And each comment records text, annotated label, related micro video and hashtag. We use three json file to split train, dev and test set.

### Download

You can download Comment Annotations from the following location:

- Google Drive:[Comment Annotations Download Link](https://drive.google.com/drive/folders/1H1qUc6UCYWdg6NK9n4BwqM5aCCVM5dcF?usp=sharing)
- Baidu NetDisk:[Comment Annotations Download Link](https://pan.baidu.com/s/19K-7D4cFrY0lkhuwEVU1pg?pwd=sykw) Extract code: sykw

## Folder Structure
The folder structure of the dataset is as follows:
```
.
├── lable_data_dict.json
├── emotion_label_map.json
├── opinion_label_map.json
├── train_set.json
├── dev_set.json
├── test_set.json
└── video_feature
    ├── XXX
    └── ...
```

### lable_data_dict.json
The `lable_data_dict.json` file includes annotated data for all micro-video comments. The JSON file stores comment data in the following format:

```json
{
    "data_id_1": {
        "video_file_id": "XXXX",  // Reference to the video feature ID
        "comment": "XXXX",        // Text content of the comment
        "opinion_label": "negative",  // Opinion label
        "emotion_label": "disgust",   // Emotion label
        "hashtag": "XXXX"         // Associated hashtag
    },
    "data_id_2": {
        "video_file_id": "XXXX",
        "comment": "XXXX",
        "opinion_label": "positive",
        "emotion_label": "joy",
        "hashtag": "XXXX"
    },
    ...
}
```

In this structure:
- `data_id_x` is a unique identifier for each comment data entry.
- `video_file_id` references the ID of the corresponding video feature.
- `comment` contains the text of the comment.
- `opinion_label` categorizes the opinion expressed in the comment (e.g., "positive", "negative").
- `emotion_label` categorizes the emotion conveyed by the comment (e.g., "joy", "disgust").
- `hashtag` includes any associated hashtags relevant to the comment.


The files `emotion_label_map.json` and `opinion_label_map.json` store mappings between label names and numerical values for use in data processing. Here are the contents and structures of these files:

### emotion_label_map.json
```json
{
    "joy": 0,
    "disgust": 1,
    "surprise": 2,
    "sadness": 3,
    "trust": 4,
    "fear": 5,
    "anger": 6,
    "anticipation": 7
}
```

### opinion_label_map.json
```json
{
    "positive": 0,
    "neutral": 1,
    "negative": 2
}
```

In these structures:
- The keys are the label names (e.g., "joy", "negative").
- The values are the corresponding numerical representations used by the program to read and process the dataset.

The files `train_set.json`, `dev_set.json`, and `test_set.json` represent the splits of the dataset, partitioned randomly in a 7:1:2 ratio. These files contain lists of comment data IDs that correspond to entries in the `lable_data_dict.json` file.

### train_set.json
```json
[
    "data_id_1",
    "data_id_2",
    "data_id_3",
    ...
]
```

### dev_set.json
```json
[
    "data_id_8",
    "data_id_9",
    "data_id_10",
    ...
]
```

### test_set.json
```json
[
    "data_id_15",
    "data_id_16",
    "data_id_17",
    ...
]
```

In these structures:
- Each file contains a list of unique comment data IDs.
- These IDs correspond to the entries in `lable_data_dict.json`, thus allowing the program to fetch the full comment data for training, development, and testing purposes.


The `video_feature` folder contains feature representations of the micro-videos. Each subfolder is named after a different feature extraction method, and the features for each video are saved as `.npy` files. The filenames correspond to the `video_file_id`. Currently, features extracted using I3D and VideoMAE methods have been released, with more features, including ResNet, to be released in the future.

### Structure of the `video_feature` folder:
```
video_feature/
    ├── I3D/
    │   ├── video_file_id_1.npy
    │   ├── video_file_id_2.npy
    │   └── ...
    ├── VideoMAE/
    │   ├── video_file_id_1.npy
    │   ├── video_file_id_2.npy
    │   └── ...
    └── ...
        └── ResNet/ (to be released)
            ├── video_file_id_1.npy
            ├── video_file_id_2.npy
            └── ...
```

In this structure:
- Each subfolder (e.g., `I3D`, `VideoMAE`) contains `.npy` files representing the features of the videos extracted using the respective method.
- The `.npy` files are named with the `video_file_id`, ensuring a direct correspondence with the `video_file_id` in `lable_data_dict.json`.


## License

 Our code is open sourced under the MIT license. Our annotations are available under a CC BY-SA 4.0 license.

If you have any questions about this repository or the datasets, please contact us.

Thank you!

# Data Collection Script

This code repository contains a script for capturing and saving images from a video stream. It allows you to create directories for positive and negative samples, and captures frames from a video to save as image samples.

## Installation

To run this code, you need to install the following libraries:

- OpenCV (opencv-python)
- Pandas
- Numpy
- Matplotlib

You can install these libraries by running the following commands:

```python
!pip install opencv-python
!pip install pandas
!pip install numpy
!pip install matplotlib
```

## Directory Setup

Before running the image capture script, you need to create directories to store the captured images. The script assumes that the directories are located in the Google Drive folder.

First, mount your Google Drive by running the following command:

```python
from google.colab import drive
drive.mount('/content/gdrive')
```

Then change the current working directory to the desired location for data collection:

```python
%cd /content/gdrive/My Drive/Colab Notebooks/Data Collection
```

Specify the directory paths for positive and negative samples:

```python
# Directory for Positive Samples
POS_PATH = os.path.join('data', 'positive')

# Directory for Negative Samples
NEG_PATH = os.path.join('data', 'negative')
```

## Image Capture Script

The code captures frames from a video and provides options to save the frames as positive or negative samples.

To capture images, run the following code:

```python
cap = cv2.VideoCapture('Fela Kuti Test video.mp4')

while(cap.isOpened()):
    ret, frame = cap.read()
    cv2.imshow('frame', frame)

    # Collect Negative images
    if cv2.waitKey(1) & 0xFF == ord('n'):
        imgname = os.path.join(NEG_PATH, '{}.jpg'.format(uuid.uuid1()))
        resizedNegative = cv2.resize(frame, (250, 250), interpolation=cv2.INTER_AREA)
        cv2.imwrite(imgname, resizedNegative)

    # Collect positive images
    if cv2.waitKey(1) & 0xFF == ord('p'):
        imgname = os.path.join(POS_PATH, '{}.jpg'.format(uuid.uuid1()))
        resizedPositive = cv2.resize(frame, (250, 250), interpolation=cv2.INTER_AREA)
        cv2.imwrite(imgname, resizedPositive)

    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

# Press the N key to capture negative samples from the video
# Press the P key to capture positive samples from the video

cap.release()
cv2.destroyAllWindows()
```

While running the code, a video stream will open, and you can press the following keys to capture images:

- N key: Capture a negative image (saved in the negative samples directory).
- P key: Capture a positive image (saved in the positive samples directory).
- Q key: Quit the image capture script.

Make sure to replace `'Fela Kuti Test video.mp4'` with the path or name of your video file.

That's it! You can use this script to collect image samples from a video stream for various purposes.

# 103 Website: Live Object Detection Demo

A small Flask web app that streams your webcam to the browser with live object detection drawn on top. It uses a pretrained YOLOv5s model and shows bounding boxes with labels and confidence scores.

## What it does

- `/` serves the landing page.
- `/video` serves the live video page.
- `/video_feed` is the MJPEG stream the video page displays. Each webcam frame is run through YOLOv5s, and detections are drawn as green boxes with a label and confidence.

Detection is limited to these COCO classes: person, bicycle, car, motorcycle, bus, train, truck, traffic light, stop sign, cat and dog.

## Where things are

The app's code was committed inside the `.venv` folder, so the layout is unusual:

| Path | Contents |
| --- | --- |
| `.venv/app.py` | Flask app and routes |
| `.venv/camera.py` | `VideoCamera`: opens the webcam, loads YOLOv5s through `torch.hub`, draws detections |
| `.venv/templates/` | `index.html` and `livevideo.html` |
| `images/` | Four photos (not referenced by the current templates) |
| `yolov5s.pt` | YOLOv5s weights |

The virtual environment committed alongside it was created on macOS and won't work on another machine, so create your own.

## Running

Requires Python 3 and a webcam.

```bash
python3 -m venv env
source env/bin/activate        # Windows: env\Scripts\activate
pip install flask torch opencv-python numpy
python .venv/app.py
```

Then open http://127.0.0.1:5000. The first run downloads the YOLOv5 code from GitHub through `torch.hub`, so you need an internet connection, and the server grabs webcam device 0 as soon as it starts.

## Tech

Python, Flask, OpenCV, PyTorch, YOLOv5.

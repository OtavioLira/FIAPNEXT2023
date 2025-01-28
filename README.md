# FIAPNEXT2023

![Project Image](project-image-url)

### Table of Contents
You're sections headers will be used to reference location of destination.

- [Description](#description)
- [How To Use](#how-to-use)
- [References](#references)
- [License](#license)
- [Author Info](#author-info)

---

## Description

This project was developed during NEXT 2023 at FIAP. We built a drone equipped with computer vision for detecting tractor parts. Sponsored by John Deere, we used ESP-32 CAM, a drone, tractor parts, Google Drive, Python, and the YOLOv5 library.

#### Technologies

- **ESP-32 CAM** (Arduino)
- **Cloud Storage** (Google Drive)
- **Python**
- **YOLOv5 Library**

## Not necessary
- **Drone**
- **Tractor Parts** (Why would you want tractor parts?)


[Back To The Top](#fiapnext2023)

---

## How To Use

#### Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/ultralytics/yolov5.git
   ```
2. Install dependencies:
   ```bash
   pip install -r yolov5/requirements.txt
   ```
3. Add your custom configuration and data files:
   - Copy your YAML file:
     ```bash
     cp /content/drive/MyDrive/TRATOR/trator.yaml yolov5/data
     ```
   - Copy images and labels:
     ```bash
     cp -r /content/drive/MyDrive/TRATOR/images /content
     cp -r /content/drive/MyDrive/TRATOR/labels /content
     cp -r /content/drive/MyDrive/TRATOR/test /content
     ```

4. Resize images for training and validation:
   ```python
   from PIL import Image
   import os

   # Resize training images
   input_folder = "/content/images/treino"
   output_folder = "/content/images/train"
   target_size = (360, 640)

   for filename in os.listdir(input_folder):
       img = Image.open(os.path.join(input_folder, filename))
       img = img.resize(target_size, Image.ANTIALIAS)
       img.save(os.path.join(output_folder, filename))

   # Resize validation images
   input_folder = "/content/images/validacao"
   output_folder = "/content/images/val"

   for filename in os.listdir(input_folder):
       img = Image.open(os.path.join(input_folder, filename))
       img = img.resize(target_size, Image.ANTIALIAS)
       img.save(os.path.join(output_folder, filename))
   ```

#### Training

Run the training script:
```bash
python yolov5/train.py --data trator.yaml --weights yolov5s.pt --img 640 --epochs 40
```

#### Detection

1. Locate the latest training run:
   ```python
   import os
   import subprocess

   def get_latest_train_run_folder():
       subfolders = [f.path for f in os.scandir('/content/yolov5/runs/train') if f.is_dir()]
       latest_folder = max(subfolders, key=os.path.getctime, default=None)
       return latest_folder

   latest_run = get_latest_train_run_folder()
   ```

2. Run detection using the best model:
   ```bash
   python /content/yolov5/detect.py --weights {latest_run}/weights/best.pt --img 640 --source /content/test --data /content/yolov5/data/trator.yaml
   ```

[Back To The Top](#fiapnext2023)

---

## References

- [YOLOv5 Documentation](https://github.com/ultralytics/yolov5)
- [Pillow Documentation](https://pillow.readthedocs.io/en/stable/)
- [ESP-32 CAM Setup](https://randomnerdtutorials.com/esp32-cam-projects-esp32-camera/)

[Back To The Top](#fiapnext2023)

---

## License

MIT License

Copyright (c) [2024] [Otávio Lira Neves]

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

[Back To The Top](#fiapnext2023)

---

## Author Info

- Linkedin - [Otávio Lira Neves](https://www.linkedin.com/in/otavioliraneves/)
- Gmail - [Otávio Lira Neves](otavioliraneves@gmail.com)

[Back To The Top](#fiapnext2023)


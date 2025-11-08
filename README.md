
# Language-to-Segment&Track

Language-driven visual segmentation and object tracking system based on [Grounding-DINO](https://github.com/IDEA-Research/GroundingDINO) and [SAMURAI](https://github.com/yangchris11/samurai).

---
### 🔥 News

- **`2025/07/31`**: Support continuous detection, tracking, and segmentation of individual category objects through text prompts. Optimize the old data release logic to reduce memory footprint and improve the running speed of interactive inference.
- **`2025/07/19`**: Supports backward tracking of each object.
- **`2025/05/08`**: Optimize memory usage and code structure.
- **`2025/04/29`**: Initial version submission.

---

### 🔍 What Can It Do?

#### For Video Files or Real-Time Video (Camera):
> Default camera supported is Intel RealSense. For others, please modify the video capture method manually.
- Allows initializing multiple object tracks via **'bbox prompts'**, **'point prompts'**, and **'mask prompts'** in the first frame.
- Enables **interactive tracking and segmentation** on any frame using:
  - Mouse click
  - Manual box drawing
  - Text prompt
- Tracked objects added at any frame can be tracked backwards to the untracked frames after the forward tracking is completed, and finally the complete **'mask trace'** of each object is obtained.
- Support continuous detection, tracking, and segmentation of individual category objects through text prompts.

https://github.com/user-attachments/assets/40a340c7-d818-493f-b86a-bb8ed5ca517c


https://github.com/user-attachments/assets/c709131f-be66-4952-b8e2-b95fbab6529d


#### For Images:
- Accepts a text prompt and returns (Supports **batch processing** of images):
  - Label
  - Score
  - Bounding Box
  - Segmentation Mask

![](assets/Figure_1.png)

---

## 🚀 Get Started

We recommend using **Anaconda** for environment management.

### ✅ Prerequisites

- OS: Ubuntu >= 18.04  
- NVIDIA Driver (`nvidia-smi`) >= **550**

---

### 🛠 Installation

```bash
git clone https://github.com/wngkj/Lang2SegTrack.git
cd Lang2SegTrack

conda create -n lang2segtrack python=3.10
conda activate lang2segtrack

pip install torch==2.4.1 torchvision==0.19.1 --extra-index-url https://download.pytorch.org/whl/cu124

cd models/sam2
pip install -e .
pip install -e ".[notebooks]"

cd ../gdino
pip install -e .
```

---

### 📦 Download SAM2.1 Checkpoints

Place them into `sam2/checkpoints/`:

- [sam2.1_hiera_tiny](https://dl.fbaipublicfiles.com/segment_anything_2/092824/sam2.1_hiera_tiny.pt)
- [sam2.1_hiera_small](https://dl.fbaipublicfiles.com/segment_anything_2/092824/sam2.1_hiera_small.pt)
- [sam2.1_hiera_base_plus](https://dl.fbaipublicfiles.com/segment_anything_2/092824/sam2.1_hiera_base_plus.pt)
- [sam2.1_hiera_large](https://dl.fbaipublicfiles.com/segment_anything_2/092824/sam2.1_hiera_large.pt)

---

## Usage


  ```bash
  python scripts/lang2segtrack.py
  ```
- **`track`**: Track objects in video files or real-time video streams by using first-frame prompts, text-prompts, mouse click(Ctrl + left) or manual boxes drawing. If you need a higher frame rate and don't need the text prompt feature, set it`use_txt_prompt=False`. You can also increase the tracking frame rate by setting the `image_size` parameter in the config file(`sam2/configs/samurai/`) to which the model belongs, for example, to 512.


- **`predict_img`**: Predict objects in images by using text-prompts.


  ```bash
  python scripts/lang2segtrack_with_backward.py
  ```
- **`track`**: Supports backward tracking after the forward tracking is completed, and finally returns the tracking data 'mask' of each tracked object in the entire video stream.


  ```bash
  python scripts/lang2segtrack_keep_detection.py
  ```
- **`track`**: Support continuous detection, tracking, and segmentation of individual category objects in video streams through text prompts. (The **'trial version'** only uses the IOU to manage new and old objects, and subsequent versions will use more efficient and accurate method. This script contains all the functions of the aforementioned script, but this script is demanding on device performance, and if there is no need for continuous tracking, it is recommended to use `lang2segtrack.py` or `lang2segtrack_with_backward.py`.)

---

## 🙏 Acknowledgments

This project builds upon outstanding prior work:

- [Grounding-DINO](https://github.com/IDEA-Research/GroundingDINO)
- [SAMURAI](https://github.com/yangchris11/samurai)
- [SAM2](https://github.com/facebookresearch/sam2)
- [Language-Segment-Anything](https://github.com/luca-medeiros/lang-segment-anything)

## Citation
If you find this project useful, please consider citing:
```bibtex
@misc{lang2segtrack,
  title = {Language-to-Segment&Track},
  howpublished = {\url{https://github.com/wngkj/Lang2SegTrack}},
  author = {Kejie Wang},
  year = {2025}
  }
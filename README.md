# Social Distancing Early Forecasting System

Out-of-the-box code base for social distancing early forecasting. Given a video, this code will give out a warning if the system predicts that people will violate social distancing (getting closer with each other than 6 feet) in the next 5 seconds. This early warnings could help stop people before they are actually at risk of getting infected. See this [blog](https://medium.com/@junweil/social-distancing-early-forecasting-system-60186baa67f5).

Keep social distancing (about 6 feet) and [save lives](https://www.cdc.gov/)!

Below we show an example of the system output. If potential risks are detected, trajectory predictions are shown and warnings are printed near the person.

<div align="center">
  <div style="">
      <img src="images/VIRAT_S_000008.short.crop.gif" width="600px" />
  </div>
  <br/>
</div>


## Dependencies
+ Python 2/3; TensorFlow-GPU==1.15.2; cv2; tqdm; scipy; sklearn; matplotlib; ffmpeg

## Usage
### Step 1: Download models and a test video
Assuming you run the code at the top level of this repository. Model size is about 468MB and the test video is about 7MB.
```
bash scripts/download_models.sh
bash scripts/download_test_video.sh
```

### Step 2: Run inferencing
```
python code/inference/main.py test/test_videos.lst test/output --pred_vis_path test/visualization
```

### Step 3: Make a video
```
cd test/visualization
ffmpeg -framerate 30.0 -i test_video/test_video_F_%08d.jpg test_video.mp4
```

## Speed
My limited tests show that on a RTX 2060 (6GB memory) the processing time is 2x real-time, which means a one-minute 1920x1080 video will take 2 minute to process.
On a GTX 1080 TI it is about 1x real-time.
Reducing input resolution will significantly decrease the processing time.
The visualization is slow since it writes tons of images to the disk.

## Acknowledgments
This project is based on [CMU's Object Detection and Tracking](https://github.com/JunweiLiang/Object_Detection_Tracking) and the following papers.
If you find this code useful then please cite:
```
@inproceedings{liang2019peeking,
  title={Peeking into the future: Predicting future person activities and locations in videos},
  author={Liang, Junwei and Jiang, Lu and Niebles, Juan Carlos and Hauptmann, Alexander G and Fei-Fei, Li},
  booktitle={Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition},
  pages={5725--5734},
  year={2019}
}
@inproceedings{liang2020garden,
  title={The Garden of Forking Paths: Towards Multi-Future Trajectory Prediction},
  author={Junwei Liang and Lu Jiang and Kevin Murphy and Ting Yu and Alexander Hauptmann},
  booktitle={Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition},
  year={2020}
}
```

## More Examples
<div align="center">
  <div style="">
      <img src="images/VIRAT_S_040104_04_000854_000934.crop.gif" width="600px" />
  </div>
  <br/>
  <div style="">
      <img src="images/VIRAT_S_000201_05_001081_001215.crop.gif" width="600px" />
  </div>
  <br/>
  <div style="">
      <img src="images/VIRAT_S_040104_01_000227_000457.crop.gif" width="500px" />
  </div>
</div>


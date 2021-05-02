# NTIRE 2021 Challenge on Quality Enhancement of Compressed Video

The homepage for the NTIRE 2021 Challenge on Video Enhancement.  [[Dataset report]](https://arxiv.org/abs/2104.10782) [[Methods report]](https://arxiv.org/abs/2104.10781) 

This challenged is organized by [Ren Yang](https://renyang-home.github.io/) and [Dr. Radu Timofte](https://people.ee.ethz.ch/~timofter/) (ETH Zurich) as a part of the [NTIRE workshop](https://data.vision.ee.ethz.ch/cvl/ntire21/) in conjunction with [CVPR 2021](http://cvpr2021.thecvf.com/workshops-schedule).

If the LDV dataset and the benchmark are useful for your research, please cite:
```
@inproceedings{yang2021dataset,
  title={{NTIRE 2021} Challenge on Quality Enhancement of Compressed Video: Dataset and Study},
  author={Ren Yang and Radu Timofte}, 
  booktitle={IEEE/CVF Conference on Computer Vision and Pattern Recognition Workshops}, 
  year={2021}
}

@inproceedings{yang2021ntire,
  title={{NTIRE 2021} Challenge on Quality Enhancement of Compressed Video: Methods and Results},
  author={Ren Yang and Radu Timofte and others}, 
  booktitle={IEEE/CVF Conference on Computer Vision and Pattern Recognition Workshops}, 
  year={2021}
}
```

If you have questions, find dead links or bugs, please feel free to contact:

Ren Yang @ ETH Zurich, Switzerland   

Email: ren.yang@vision.ee.ethz.ch

## Large-scale Diverse Video (LDV) Dataset

The proposed LDV dataset is used in the NTIRE 2021 challenge. It currently contains 240 videos with diverse categories of content, different kinds of motion and various frame-rates. The dataset may be further extended in the future. The details of the proposed LDV dataset are discribed in the dataset report:

> Ren Yang and Radu Timofte, "NTIRE 2021 Challenge on Quality Enhancement of Compressed Video: Dataset and Study", in IEEE/CVF Conference on Computer Vision and Pattern Recognition Workshops, 2021. [[Paper]](https://arxiv.org/abs/2104.10782)

### Download the LDV dataset

- Training set (200 videos) 
[[Raw]](https://data.vision.ee.ethz.ch/reyang/training_raw.zip) 
[[Fixed QP]](https://data.vision.ee.ethz.ch/reyang/training_fixed-QP.zip)
[[Fixed bit-rate]](https://data.vision.ee.ethz.ch/reyang/training_fixed-rate.zip)
[[Info]](https://data.vision.ee.ethz.ch/reyang/data_train.xlsx)

- Validation set (20 videos)
[[Raw]](https://data.vision.ee.ethz.ch/reyang/validation_raw.zip)
[[Fixed QP]](https://data.vision.ee.ethz.ch/reyang/validation_fixed-QP.zip)
[[Fixed bit-rate]](https://data.vision.ee.ethz.ch/reyang/validation_fixed-rate.zip)
[[Info]](https://data.vision.ee.ethz.ch/reyang/data_validation.xlsx)

- Test set for Tracks 1 and 2 (10 videos)
[[Raw]](https://data.vision.ee.ethz.ch/reyang/test_raw_1.zip)
[[Fixed QP]](https://data.vision.ee.ethz.ch/reyang/test_fixed-QP_release.zip)
[[Fixed bit-rate]](https://data.vision.ee.ethz.ch/reyang/test_fixed-rate_1.zip)
[[Info]](https://data.vision.ee.ethz.ch/reyang/data_test_1.xlsx)

- Test set for Track 3 (10 videos)
[[Raw]](https://data.vision.ee.ethz.ch/reyang/test_raw_2.zip)
[[Fixed QP]](https://data.vision.ee.ethz.ch/reyang/test_fixed-QP_2.zip)
[[Fixed bit-rate]](https://data.vision.ee.ethz.ch/reyang/test_fixed-rate_release.zip)
[[Info]](https://data.vision.ee.ethz.ch/reyang/data_test_2.xlsx) 

The NTIRE 2021 challenge evaluates methods in the **RGB domain**. Hence, please convert the mkv videos to png images for test and evaluation:

```
ffmpeg -i xxx.mkv ./xxx/%3d.png
```

### Compression configurations

#### Tracks 1 and 2 (fixed QP)

In Tracks 1 and 2, videos are compressed in the YUV domain by the Low-delay P mode HM 16.20 at QP 37. The raw YUV videos are losslessly compressed to mkv via ffmpeg x265 to reduce the file sizes.

1. To reproduce the compression of data, please first convert mkv files to YUV domain. The ffmpeg x265 decoder is recommended, e.g., “ffmpeg -i 001.mkv -pix_fmt yuv420p 001.yuv”

2. Download HM 16.20 at https://hevc.hhi.fraunhofer.de/svn/svn_HEVCSoftware/tags/HM-16.20 or https://data.vision.ee.ethz.ch/reyang/HM16.20.zip

3. Compress yuv files by the command:
```
path_to_HM16.20/bin/TAppEncoderStatic
-c path_to_HM16.20/cfg/encoder_lowdelay_P_main.cfg
-c path_to_HM16.20/cfg/per-sequence/BasketballDrill.cfg
-i xxx.yuv -q 37 -wdt (width) -hgt (height) -f (frame_num) -fr (frame_rate)
-b xxx.mkv
```
Note that “BasketballDrill.cfg” is a randomly selected file, and most of its information are replaced by the following configurations. Width, height, frame number and frame rate values are available in the info excel files (refer to the links above).

4. The quality is evaluated in the RGB domain by PSNR. Please convert raw, compressed (and enhanced) videos to RGB domain for evaluation, e.g.,
```
ffmpeg -i path_to_raw/001.mkv ./raw_001/%3d.png
ffmpeg -i path_to_compressed/001.mkv ./001/%3d.png
```

#### Track 3 (fixed bit-rate)

In this track, videos are compressed in the YUV domain by x265 of ffmpeg 4.3.1 at 200kbps. The raw YUV videos are losslessly compressed to mkv via ffmpeg x265 to reduce the file sizes.

1. To reproduce the compression of data, please first convert mkv files to YUV domain. The ffmpeg x265 decoder is recommended, e.g., “ffmpeg -i 001.mkv -pix_fmt yuv420p 001.yuv”

2. Download ffmpeg 4.3.1 at https://johnvansickle.com/ffmpeg/releases/ffmpeg-release-amd64-static.tar.xz or https://data.vision.ee.ethz.ch/reyang/ffmpeg-release-amd64-static.tar.xz
 
3. Compress yuv files at 200kbps via the two-pass rate control strategy, which ensures an accurate rate control:
```
ffmpeg -pix_fmt yuv420p -s (width)x(height) -r (frame_rate) -i xxx.yuv -c:v libx265 -b:v 200k -x265-params pass=1:log-level=error -f null /dev/null
ffmpeg -pix_fmt yuv420p -s (width)x(height) -r (frame_rate) -i xxx.yuv -c:v libx265 -b:v 200k -x265-params pass=2:log-level=error xxx.mkv
```

Note that width, height, frame number and frame rate values are available in the info excel files (refer to the links above).

4. The quality is evaluated in the RGB domain by PSNR. Please convert raw, compressed (and enhanced) videos to RGB domain for evaluation, e.g.,
```
ffmpeg -i path_to_raw/001.mkv ./raw_001/%3d.png
ffmpeg -i path_to_compressed/001.mkv ./001/%3d.png
```

## NTIRE 2021 Benchmark

The methods and results of the NTIRE 2021 benchmark are discribed in the methods report:

> Ren Yang, Radu Timofte, et al., "NTIRE 2021 Challenge on Quality Enhancement of Compressed Video: Methods and Results", in IEEE/CVF Conference on Computer Vision and Pattern Recognition Workshops, 2021. [[Paper]](https://arxiv.org/abs/2104.10781)

To make the benchmark more convincing and solid, we will update the open source codes of the proposed methods in the following.

### Papers, codes and models (keep updating)

- **BILIBILI AI & FDU Team** (Contact: Jing Liu & Yi Xu, liujing04@bilibili.com, yxu17@fudan.edu.cn)

  Winner of Tracks 1 and 2, Runner-up of Track 3

  - Code: (may release later)

- **NTU-SLab Team** (Contact: Kelvin C.K. Chan, chan0899@e.ntu.edu.sg)

  Winner of Tracks 1 and 3, Runner-up of Track 2
  
  Good neneralization, Good trade-off between running time and PSNR
  
  - Paper: https://arxiv.org/abs/2104.13371

  - Code: (may release later to MMEditing)
  
- **VUE Team** (Contact: Xin Li & He Zheng, lixin41@baidu.com, zhenghe01@baidu.com)

  - Paper for Track 2: (may be published later)

- **NJU-Vision Team** (Contact: Ming Lu, luming@smail.nju.edu.cn)

  - Code for Track 1: https://github.com/lumingzzz/QENet

- **VIP&DJI Team** (Contact: Hai Wang, wanghai19@mails.tsinghua.edu.cn)

  - Code for Track 1: https://github.com/yiyunchen/CVQENet

  - Code for Track 3: https://github.com/littlewhitesea/NTIRE2021_compressed_video_enhancement

- **Shannon Team** (Contact: Dewang Hou, dewh@pku.edu.cn)

  - Code: (may release later)

- **HNU_CVers Team** (Contact: Yucong Wang, 1401121556@qq.com)

  - Code: https://github.com/wnxbwyc/RCVN-For-Video-Enhancement

- **Ivp-tencent Team** (Contact: Xiaoyu Zhang, zxy2019@pku.edu.cn)

  Most time-efficient method (120 fps with better quality performance then the baseline models)

  - Code for Track 1: https://github.com/zxy110/BRNet 
  
- **BOE-IOT-AIBD Team** (Contact: Pablo Navarrete Michelini, pnavarre@ieee.org)

  - Related paper: https://arxiv.org/abs/2101.00150

- **MFQE, QE-CNN, DnCNN, and ARCNN** (Contact: Ren Yang, ren.yang@vision.ee.ethz.ch)

  Baseline models

  - Code for Track 1: https://github.com/RenYang-home/NTIRE21_VEnh_Baseline


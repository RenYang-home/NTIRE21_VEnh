# NTIRE 2021 Challenge on Quality Enhancement of Compressed Video

The homepage for the NTIRE 2021 Challenge on Quality Enhancement of Compressed Video. If the LDV dataset and the benchmark are useful for your research, please cite:
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

The proposed LDV dataset is used in the NTIRE 2021 challenge. It contains 240 videos with diverse categories of content, different kinds of motion and various frame-rates. The details of the proposed LDV dataset are discribed in the dataset report:

> Ren Yang and Radu Timofte, "NTIRE 2021 Challenge on Quality Enhancement of Compressed Video: Dataset and Study", in IEEE/CVF Conference on Computer Vision and Pattern Recognition Workshops, 2021. [[Paper]](https://arxiv.org/abs/2104.10782)

#### Training set (200 videos)

Raw: https://data.vision.ee.ethz.ch/reyang/training_raw.zip

Fixed QP: https://data.vision.ee.ethz.ch/reyang/training_fixed-QP.zip

Fixed bit-rate: https://data.vision.ee.ethz.ch/reyang/training_fixed-rate.zip

Info: https://data.vision.ee.ethz.ch/reyang/data_train.xlsx (resolution, frame-rate, etc.)

#### Validation set (20 videos)

Raw: https://data.vision.ee.ethz.ch/reyang/validation_raw.zip

Fixed QP: https://data.vision.ee.ethz.ch/reyang/validation_fixed-QP.zip

Fixed bit-rate: https://data.vision.ee.ethz.ch/reyang/validation_fixed-rate.zip

Info: https://data.vision.ee.ethz.ch/reyang/data_validation.xlsx (resolution, frame-rate, etc.)

#### Test set for Tracks 1 and 2 (10 videos)

Raw: https://data.vision.ee.ethz.ch/reyang/test_raw_1.zip

Fixed QP: https://data.vision.ee.ethz.ch/reyang/test_fixed-QP_release.zip

Fixed bit-rate: https://data.vision.ee.ethz.ch/reyang/test_fixed-rate_1.zip (not used in the challenge)

Info: https://data.vision.ee.ethz.ch/reyang/data_test_1.xlsx (resolution, frame-rate, etc.)

#### Test set for Track 3 (10 videos)

Raw: https://data.vision.ee.ethz.ch/reyang/test_raw_2.zip

Fixed QP: https://data.vision.ee.ethz.ch/reyang/test_fixed-QP_2.zip (not used in the challenge)

Fixed bit-rate: https://data.vision.ee.ethz.ch/reyang/test_fixed-rate_release.zip

Info: https://data.vision.ee.ethz.ch/reyang/data_test_2.xlsx (resolution, frame-rate, etc.)

## NTIRE 2021 Benchmark

The methods and results of the NTIRE 2021 benchmark are discripted in the methods report:

> Ren Yang, Radu Timofte, et al., "NTIRE 2021 Challenge on Quality Enhancement of Compressed Video: Methods and Results", in IEEE/CVF Conference on Computer Vision and Pattern Recognition Workshops, 2021. [[Paper]](https://arxiv.org/abs/2104.10781)

To make the benchmark more convincing and solid, we will update the open source codes of the proposed methods in the following.

### Codes and Models

BILIBILI AI & FDU Team: Winner of Tracks 1 and 2

Code: (may release later)

NTU-SLab Team: Winner of Tracks 1 and 3

Code: (may release later)


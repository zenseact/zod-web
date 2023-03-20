---
permalink: /
title:  "Home"
categories: jekyll update
header:
  image: /assets/images/header.jpg
carousels:
  - images:
    - image: /assets/images/dynamic_objects.jpg
    - image: /assets/images/static_objects.jpg
    - image: /assets/images/lane_markings.jpg
    - image: /assets/images/ego_road.jpg
---

# Zenseact Open Dataset
The **Zenseact Open Dataset** (ZOD) is a large multi-modal autonomous driving (AD) dataset, created by researchers at Zenseact. It was collected over a 2-year period in 14 different European counties, using a fleet of vehicles equipped with a full sensor suite. The dataset consists of three subsets: [*Frames*](/frames), [*Sequences*](/sequences), and [*Drives*](/drives), designed to encompass both data diversity and support for spatiotemporal learning, sensor fusion, localization, and mapping.

*Frames* consist of 100k curated camera images with two seconds of other supporting sensor data, while the 1473 *Sequences* and 29 *Drives* include the entire sensor suite for 20 seconds and a few minutes, respectively. To see examples from each of the subsets, please visit their respective pages.

**Noteably**, ZOD is currently the only AD dataset released under the permissive `CC BY-SA 4.0` license, allowing for both commercial and non-commercial use. We believe that this will help the community to advance the state-of-the-art in autonomous driving as it can enable smaller companies to use the dataset for research, benchmarking, and development. For more information about the license, see [here](/license).

## Annotations
Together with our dataset, we also release a comprehensive set of annotations for several different tasks. For more detailed information about the annotations, visit the [Annotations](/annotations) page. In summary, the following annotations are provided:
- **Objects**: 2D and 3D bounding boxes for static and dynamic objects in the scene.
- **Lane markings**: Instance and semantic segmentation of lane markings and road paintings.
- **Ego road**: Semantic segmentation of ego-road
- **Traffic signs**: Classification labels with a taxonomy of 156 different traffic sign classes.
- **Road condition**: Classification of the road-surface condition (e.g., wet or snow).

The images below show examples of the annotations for the different tasks.
 {% include carousel.html height="45" unit="%" number="1" %}

## Sensor setup
![Sensor setup](/assets/images/sensor_positions.png){: .align-right width="50%"}
The data collection has been conducted using several vehicles with an identical sensor layout driven around Europe over two years. The cars are equipped with a **high-resolution camera**, **3x LiDARs**, a **high-precision GNSS/IMU** sensor and other consumer-grade sensors. The sensor setup is outlined in the figure to the right and each sensor is described in more detail below.
##### Camera: 1x 120&deg; FOV 3848x2168 RGB camera.
The camera data is captured by high-resolution (8MP) wide-angle fish-eye lenses. All raw captured camera data is converted to RGB images using an internal production-level image signal processor. The RGB camera images are captured at `10Hz` and provided as `jpg` files. However, if requested, we can also provide lossless `png` files.
##### LiDAR: 1x Velodyne VLS128 and 2x Velodyne VLP16.

The LiDAR point clouds are captured at `10Hz` and stored in a standard binary file format (`.npy`) per scan. Each file contains data from all three LiDAR sensors, represented as a 6-dimensional vector with the timestamp, 3D coordinates (`x`, `y`, and `z`), `intensity`, and `diode index`. The timestamp is relative to the frame timestamp in UTC, and the 3D coordinates are in meters. `Intensity` is a measure of the reflection magnitude ranging from `0-255`, and the `diode index` specifies the emitter that produced the point, where `[0, 128)` is the VLS128, and `[128, 144)`, `[144, 160)` is the left and right VLP-16, respectively. Each LiDAR point cloud contains around `254k` points on average and ranges up to `245m`.
##### GNSS/IMU: High-precision OxTS.
The high-precision GNSS/IMU data is logged at `100Hz` and stored as `HDF5` files. The data has a `0.01m` position accuracy, `0.03deg` pitch/roll and `0.1deg` heading accuracy. The data contain `timestamp`, `latitude`, `longitude`, `altitude`, `heading`, `pitch`, `roll`, `velocities`, `accelerations`, `angular rates`, and `poses` relative to the first `pose` in the file.
##### Vehicle data: Production-grade vehicle data
Various vehicle data are also released for *Sequences* and *Drives*. These include vehicle control signals such as `steering wheel angle`, `acceleration/brake pedal ratios`, and `turn indicator status`, as well as consumer-grade IMU and satellite positioning data. The vehicle control signals, IMU, and satellite positioning data are logged at `100Hz`, `50Hz`, and `1Hz` respectively.

## Citation
If you publish work that uses Zenseact Open Dataset, please cite our [coming soon]()

```
@misc{zod2023,
  author = {TODO},
  title = {ZOD: A large-scale and diverse multimodal dataset for autonomous driving},
  year = {2023},
  publisher = {TODO},
  journal = {TODO},
}
```
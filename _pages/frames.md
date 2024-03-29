---
permalink: /frames/
title:  "Frames"
categories: jekyll update
header:
  image: /assets/images/frames/stitched_images.jpg
layout: splash
---
<br>

# ZOD Frames
<figure class="align-right" style="width: 30%; margin-top: 0;">
  <a href="/assets/images/frames/geographical_distribution_frames.png">
  <img src="/assets/images/frames/geographical_distribution_frames.png" alt=""></a>
  <figcaption>Geographical distribution of ZOD Frames.</figcaption>
</figure>

The ZOD Frames dataset consists of `100k` annotated camera-LiDAR pairs, along with &plusmn;1-second surrounding LiDAR, and high-precision GNSS. For more detailed information about the sensor setup please visit the [Sensor setup](/#sensor-setup) section on the [Home](/) page.

ZOD Frames is a **highly diverse dataset**, with data collected from **14 European countries** over two years. The geographical distribution is shown in the figure to the right and can be seen ranging from the snowy parts of northern Sweden to the sunny countryside of Italy.

To quantitatively evaluate the geographical diversity of our dataset, we made use of the diversity area metric[^1], defined as the union of all `75m` (radius) diluted ego-poses in the dataset. Using this definition, ZOD Frames obtains an area metric of `705km²`, which could be compared to `5km²`, `17km²`, and `76km²` for nuScenes[^2], Argoverse 2[^3], and Waymo Open[^1] respectively. The dataset is also highly diverse in terms of time of day, road type, and weather, as shown in the figure below.

<figure style="width: 67%;">
  <a href="/assets/images/frames/pie_charts_diversity.png">
  <img src="/assets/images/frames/pie_charts_diversity_no_bg.png" alt=""></a>
  <figcaption>Distribution over time of day (left), road type (center), and weather (right) in ZOD Frames.</figcaption>
</figure>

ZOD contains data from various driving conditions, ranging from slow-moving city driving to high-speed highway driving. To operate a vehicle safely when driving at speeds up to `130km/h` (maximum ego-vehicle speed in ZOD is `133km/h`), it is crucial to detect objects **not only in your vicinity but also at longer distances**. To accurately perceive the environment at distances required for high-speed driving, the ego-vehicle has to be equipped with sensors with sufficient resolution to enable long-range perception. In ZOD, we have an 8MP front-looking camera coupled with high-resolution LiDAR sensors, allowing annotation of objects up to `245m` away.

To highlight this, we show the distribution of the distance to the ego-vehicle over all annotated objects in nuScenes[^2], Waymo Open[^1], Argoverse2[^3], and ZOD Frames in the figure below, where we can see that ZOD Frames has a range distribution similar to the Argoverse 2 dataset, with the exception of having a longer tail for `Vehicle` and a lower density for distant `VulnereableVehicle`.

<figure class="align-center">
  <a href="/assets/images/frames/ann_obj_dist.png">
  <img src="/assets/images/frames/ann_obj_dist.png" alt=""></a>
  <figcaption> Distribution of the distance to the ego-vehicle over all annotated objects in nuScenes, Waymo Open, Argoverse2, and ZOD Frames.</figcaption>
</figure>


## Annotation
<figure class="align-right" style="width: 30%; margin-top:0;">
  <a href="/assets/images/frames/project_counts.png">
  <img src="/assets/images/frames/project_counts.png" alt=""></a>
  <figcaption>The amount of annotated Frames per project.</figcaption>
</figure>

The ZOD Frames dataset is fully annotated (i.e., every *Frame*) for the `Objects`, `Lanes`, and `Road Condition` annotation tasks. Moreover, roughly 67% of all Frames are also annotated for the `Traffic Signs` and `Ego Road` annotation tasks, see the figure to the right. For more detail on each of the annotation tasks, please refer to the [Annotation](/annotations) page.

**Note** that we provide annotations for the camera-LiDAR pairs, but not for the surrounding LiDAR data.


## Data samples
Here, we show some data samples from the dataset. We deliberately show scenes that reflect the diversity of the dataset, including scenes where the sensors are obscured by adverse weather.

<figure class="half">
<a href="/assets/images/frames/000766_camera.jpg" title="Camera Frame #000766" alt="Camera Frame #000766">
<img src="/assets/images/frames/000766_camera.jpg"  alt=""></a>
<a href="/assets/images/frames/000766_lidar.png" title="Lidar Frame #000766" alt="Lidar Frame #000766">
<img src="/assets/images/frames/000766_lidar.png" alt=""></a>
<figcaption>Rainy scene, obscuring both camera and LiDAR. Note the hallucinated wall in the point cloud (in the front-left of the ego-vehicle) caused by water droplets on the sensor. Frame #000766.</figcaption>
</figure>

<figure class="half">
<a href="/assets/images/frames/024234_camera.jpg" title="Camera Frame #024234" alt="Camera Frame #024234">
<img src="/assets/images/frames/024234_camera.jpg" alt=""></a>
<a href="/assets/images/frames/024234_lidar.png" title="Lidar Frame #024234" alt="Lidar Frame #024234">
<img src="/assets/images/frames/024234_lidar.png" alt=""></a>
<figcaption>Crowded downtown scene. Frame #024234.</figcaption>
</figure>

<figure class="half">
<a href="/assets/images/frames/066087_camera.jpg" title="Camera Frame #066087" alt="Camera Frame #066087">
<img src="/assets/images/frames/066087_camera.jpg" alt=""></a>
<a href="/assets/images/frames/066087_lidar.png" title="Lidar Frame #066087" alt="Lidar Frame #066087">
<img src="/assets/images/frames/066087_lidar.png" alt=""></a>
<figcaption>Highway driving during heavy rain. Spray from vehicles in front hinders visibility in the camera and blocks the LiDAR. Frame #066087.</figcaption>
</figure>


<figure class="half">
<a href="/assets/images/frames/097490_camera.jpg" title="Camera Frame #097490" alt="Camera Frame #097490">
<img src="/assets/images/frames/097490_camera.jpg" alt=""></a>
<a href="/assets/images/frames/097490_lidar.png" title="Lidar Frame #097490" alt="Lidar Frame #097490">
<img src="/assets/images/frames/097490_lidar.png" alt=""></a>
<figcaption>Driving in snowy conditions during the night on a curvy road. Frame #094790.</figcaption>
</figure>

<figure class="half">
<a href="/assets/images/frames/096284_camera.jpg" title="Camera Frame #096284" alt="Camera Frame #096284">
<img src="/assets/images/frames/096284_camera.jpg" alt=""></a>
<a href="/assets/images/frames/096284_lidar.png" title="Lidar Frame #096284" alt="Lidar Frame #096284">
<img src="/assets/images/frames/096284_lidar.png" alt=""></a>
<figcaption>Driving on a road completely covered in snow. Frame #096284</figcaption>
</figure>

<figure class="half">
<a href="/assets/images/frames/058594_camera.jpg" title="Camera Frame #058594" alt="Camera Frame #058594">
<img src="/assets/images/frames/058594_camera.jpg" alt=""></a>
<a href="/assets/images/frames/058594_lidar.png" title="Lidar Frame #058594" alt="Lidar Frame #058594">
<img src="/assets/images/frames/058594_lidar.png" alt=""></a>
<figcaption>Arterial road during twilight. Frame #058594.</figcaption>
</figure>


<figure class="half">
<a href="/assets/images/frames/053409_camera.jpg" title="Camera Frame #053409" alt="Camera Frame #053409">
<img src="/assets/images/frames/053409_camera.jpg" alt=""></a>
<a href="/assets/images/frames/053409_lidar.png" title="Lidar Frame #053409" alt="Lidar Frame #053409">
<img src="/assets/images/frames/053409_lidar.png" alt=""></a>
<figcaption>Highway driving during the night. The road and vehicles are only illuminated by headlights. Frame #053409.</figcaption>
</figure>


## Additional Statistics
Here, we show some additional interesting statistics about the ZOD Frames dataset, starting with the number of annotated instances for `Objects` and `Lanes`.
<figure class="half">
  <a href="/assets/images/frames/object_counts.png">
  <img src="/assets/images/frames/object_counts.png" alt=""></a>

  <a href="/assets/images/frames/lane_counts.png">
  <img  src="/assets/images/frames/lane_counts.png" alt=""></a>
  <figcaption>The number of annotated object instances (left) and the number of lane instances (right). Note that the objects are split based on whether or not they are annotated in 2D and 3D. </figcaption>
</figure>

ZOD Frames is collected from a wide range of traffic scenarios, including downtown areas, highways, and rural roads. This results in a varying number of objects in the scene, which is shown for the top-level classes `Vehicle`, `VulnerableVehicle`, and `Pedestrian` in the figure below.

<figure class="align-center" style="width: 67%;">
  <a href="/assets/images/frames/cuboids_per_frame.png">
  <img src="/assets/images/frames/cuboids_per_frame.png" alt=""></a>
  <figcaption>The number of annotated 3D object instances per frame. </figcaption>
</figure>


[^1]: Sun, Pei, et al. <a href="https://arxiv.org/abs/1912.04838">"Scalability in perception for autonomous driving: Waymo open dataset. alt="""</a> Proceedings of the IEEE/CVF conference on computer vision and pattern recognition. 2020.
[^2]: Caesar, Holger, et al. <a href="https://arxiv.org/abs/1903.11027"> "nuScenes: A multimodal dataset for autonomous driving."<a/> Proceedings of the IEEE/CVF conference on computer vision and pattern recognition. 2020.
[^3]: Benjamin Wilson, et al. <a href="https://arxiv.org/abs/2301.00493">"Argoverse 2: Next Generation Datasets for Self-driving Perception and Forecasting alt="""</a>. In Proceedings of the Neural Information Processing Systems Track on Datasets and Benchmarks (NeurIPS Datasets and Benchmarks). 2021.
{:footnotes}

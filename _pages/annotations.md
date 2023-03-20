---
permalink: /annotations/
title:  "Annotations"
categories: jekyll update
layout: splash
---
<br>

# Annotations
On this page, we provide detailed information about the annotations that are included in our dataset. Our annotations are created by highly skilled human annotators using commercial labeling tools and have undergone a rigorous quality control process to ensure their accuracy and consistency.

The annotation companies we work with are [Kognic](https://www.kognic.com/) and [Scale](https://www.scale.com/), both of which are renowned for their expertise in providing high-quality annotations for computer vision tasks.

We supply annotations for objects, lanes, traffic signs, ego-road, and road surface, all of which are described in detail below. Note that the annotations can be easily read by using the development kit (`pip install zod`) found [here](https://github.com/zenseact/zod).

## Objects
Objects refer to static and dynamic objects **visible in the image**. These objects are annotated with a tightly fitting 2D bounding box indicated by the pixel coordinates of its four outermost points. If the object is also present in the pointcloud (range up to `245m`), the object is also annotated with a 9-DOF 3D bounding box described by the 3D-center (`x`, `y`, `z`), the 3D dimensions (`l`, `w`, `h`), and the 3D orientation quaternion (`qw`, `qx`, `qy`, `qz`).

The dynamic objects are categorized into 4 top-level classes, namely `Vehicle`, `VulnereableVehicle`, `Pedestrian`, and `Animal`. These are then further divided into 16 sub-classes, see below for a complete list. Similarly, the static objects are divided into 6 top-level classes, namely `TrafficSign`, `TrafficSignal`, `TrafficGuide`, `PoleObject`, `TrafficBeacon`, and `DynamicBarrier`. These are then further divided into 13 sub-classes, see the below for a complete list. Moreover, the `TrafficSign` class is further divided into 156 granular classes (see the [Traffic Sign](#traffic-sign) section for more details), making it the largest commercial dataset for traffic sign annotations to date.

### Object properties

| Property | Description |
|----------|-------------|
|`unclear`| This property can be set to `True` if the annotator is unsure or if we want to discard a certain area of the image. This could be if e.g., It is in some way unclear to the human eye whether or not there is an object, e.g due to the object being too small or the image being too unsharp or blurred; It is unclear whether it is a single object or if there are more than one; Several highly overlapping objects are indistinguishable in the sense that it is practically impossible to individually mark the objects; Groups of overlapping non-pedestrian objects that are **not on Ego Road** (bicycle racks with lots of bikes, distant cars on a parking lot, groups of shopping carts, herds of farm animals, etc.,)|
| `occlusion_ratio` | Estimate how much of the object that is occluded by something in the active field of view of the camera in the image, excluding any parts of the ego vehicle body and camera housing, according to the following ranges: `None`: 0%, `Light`: 1% - 20%, `Medium`: 21% - 50%, `Heavy`: 51% - 80%, `VeryHeavy`: 81% - 100%. Being seen through the windows of another vehicle does not constitute occlusion. If an object is fully seen through another vehicle’s windows it should have occlusion level `None`|
|`relative_position`| Estimate where the object is relative the ego-vehicle. Note that left and right is relative to the ego-vehicle driving direction. `BeyondLeftLane`, `LeftLane`, `LeftLane_Parked`, `LeftAndEgoLane_MainlyLeft`, `LeftAndEgoLane_MainlyEgo`, `EgoLane`, `RightAndEgoLane_MainlyRight`, `RightAndEgoLane_MainlyEgo`, `RightLane`, `RightLane_Parked`, `BeyondRightLane`, `LeftLaneOncoming`, `RightLaneOncoming`, `NotOnEgoRoad`, `Inconclusive`|
|`with_rider`| **This property is only for the `VulnereableVehicle` class.** Assign `True` if can be seen there is a rider on, or a person sitting in, the VulnerableVehicle. Assign `False` if it can beseen that there is no rider, e.g. a parked bicycle or motorcycle, or an empty wheelchair. Assign `Inconclusive` if it cannot be determined whether or not there is a person on, or in, it, e.g. if there is a baby lying in a baby stroller and therefore not visible|
|`traffic_content_visible`| **Set for all static objects**. Whether the content presented on a landmark is visible in the image. The “content” of a landmark refers to any symbols, text, reflector, light, etc. that is on the landmark. Follwing values are possbile: `True`, `False`, `Undefined`, `Inconclusive`. The combination of `class=TrafficSign` and `traffic_content_visible=True` therefor refer to a front facing traffic sign.|

### Dynamic object classes

| Top-level class | Sub-class | Comment |
|-----------------|-----------|-------------|
| `Vehicle` | `Car` | Car, SUV, Pickup, Mini-van|
| `Vehicle` | `Van` | Van, Minibus, RV/Motorhome|
| `Vehicle` | `Truck` | Truck, Truck head, Semi-trailer truck, Truck Trailer|
| `Vehicle` | `Trailer` | Includes all kinds of trailers that can be normally attached to a Car , i.e. not truck-trailers. This includes car-trailers, boat trailers, caravans, horse trailers, enclosed trailers, and roadwork trailers. This is not an exhaustive list, in general any object which is supposed to be pulled by a car is considered a trailer|
| `Vehicle` | `Bus` | -|
| `Vehicle` | `HeavyEquip` | Tractor, Excavator, Dumper|
| `Vehicle` | `TramTrain` | Tram, Train|
| `Vehicle` | `Other` | -|
| `Vehicle` | `Inconclusive` | -|
| `VulnerableVehicle` | `Bicycle` | Includes all kinds of human-powered or electric bicycles with two or more wheels.|
| `VulnerableVehicle` | `Motorcycle` | Includes all motorized two/three-wheelers, e.g. mopeds, vespas, sport-motorbikes, choppers and three wheeled motorcycles. |
| `VulnerableVehicle` | `Wheelchair` | -|
| `VulnerableVehicle` | `Stroller` |- |
| `VulnerableVehicle` | `PersonalTransporter` | Includes any human-powered, electric or motorized wheeled object that is used to transport people, such as a skateboard, segway, kick scooter, or unicycle. |
| `VulnerableVehicle` | `Other` |- |
| `VulnerableVehicle` | `Inconclusive` | -|
| `Pedestrian` | `Pedestrian` | - |
| `Animal` | `Animal` | -|

### Static object classes

| Top-level class | Sub-class | Comment |
|-----------------|-----------|-------------|
| `TrafficSign` |[Traffic signs](#traffic-signs) | Front and backfacing traffic signs. Include both electronic and classical signs.|
| `TrafficSignal` | `TrafficSignal` | Front and backfacing traffic signals. Both horizontal and vertical configurations.|
| `TrafficGuide` | `Reflector` | A reflector placed on a pole or on top of a barrier on the side of the road.|
| `TrafficGuide` | `Attention` | Highly reflective guides, which uses line segments or arrows to indicate direction or danger. These line segments can be vertical, left-leaning diagonal, right-leaning diagonal, or horizontal. These guides are commonly seen at exits, extreme curves (chevron-like), construction areas, tunnels/overpasses, and more.|
| `TrafficGuide` | `SnowMarker` | - |
| `TrafficGuide` | `Bollard` |  - |
| `TrafficGuide` | `Other` | - |
| `TrafficGuide` | `Inconclusive` | - |
| `PoleObject` | `LampPole` | - |
| `PoleObject` | `LandmarkPole` |  -|
| `PoleObject` | `LargeLandmarkPole` | -  |
| `PoleObject` | `Other` |-  |
| `PoleObject` | `Inconclusive` |  -|
| `TrafficBeacon` | `TrafficBeacon` | A single light source with a continuous state: always on, always off, or flashing. These can be seen as restrictions, for example at pedestrian crossings, or as a warning for a certain traffic condition, such as a construction site|
| `DynamicBarrier` | `DynamicBarrier` | Objects that controls the flow of cars by completely blocking the path. They are usually pole-like objects that can be positioned either horizontally to block the passage of vehicles, or vertically to allow flow of traffic. Only the part that moves and can block the flow of cars should be included in the markings. Dynamic barriers are commonly seen, but not exclusively, at railway crossings, parking lots, and bridges.|

## Lane markings & road paintings

## Traffic signs
![image-left](/assets/images/traffic_signs.jpg){: .align-right width="25%" }
The traffic sign annotations refer to the front-facing traffic signs that are visible in the image. Note that only signs related to traffic are labeled i.e., advertisement boards etc., should not be labeled. See a selection of traffic signs in the image to the right. In total, we have annotated 446k traffic sign instances across 156 classes with large variations in viewing angle, distance, lighting condition etc.
The list of classes is shown in the table below.

Note that `MaximumSpeedLimitXBegin`, `MaximumSpeedLimitXEnd`, `SpeedLimitZoneXBegin`, and `SpeedLimitZoneXEnd` are given as a range of values, where `X` is the maximum speed limit in km/h. For example, `MaximumSpeedLimit50Begin` refers to a traffic sign that indicates the beginning of a zone with a maximum speed limit of 50 km/h. These are given in range from 5 to 130 km/h in steps of 5 km/h.

| Top-level | Sub-classes |
|-----------|-------------|
| `Mandatory` | `PassOnThisSideLeft`, `PassOnThisSideRight`,  `PassOnEitherSide`, `ProceedStraightOrTurnLeft`, `ProceedStraight`, `ProceedStraightOrTurnRight`, `TurnLeftAhead`, `TurnRightAhead`, `TurnAhead`, `TurnRight`, `TurnLeft`, `Roundabout`|
|`Priority`|`GiveWay`,  `GiveWayOncoming`, `PriorityStop`, `PrioOverOncoming`, `PriorityRoadBegin`, `PriorityRoadEnd`|
|`Prohibatory`|`NoEntry`, `NoParking`, `NoStopping`, `NoUTurn`, `NoTurn`, `RoadClosed`, `NoOvertakingBegin`, `NoOvertakingEnd`, `MaximumSpeedLimitXBegin`, `MaximumSpeedLimitXEnd`, `SpeedLimitZoneXBegin`, `SpeedLimitZoneXEnd`|
|`RoadType`|`MotorwayBegin`, `MotorwayEnd`|
|`Warning`|`VulnurableRoadUserCrossing`, `VulnurableRoadUserPathWay`, `IndicationCameraSurveillance` |
|`Special`|`Children`, `Crossing`, `Cyclists`, `Animal`, `Curve`, `RoadWorkBegin`, `RoadWorkEnd`,  `Roundabout`, `TrafficSignalAhead`,  `RoadNarrows`, `RoadBump`, `RoughRoad`,  `Slippery`, `GenericWarning`, `CongestionAhead`, `TwoWayTraffic`, `MergingTraffic`, `Crossroads`, `DoubleCurve`, `TunnelAhead`|
|`Not Listed` | `Not Listed` refer to all signs that do not fall into any of the categories above.|
|`Unclear`|`Unclear` refer to a sign for which it is not possible to distinguish between the classes above.|

## Ego road

## Road surface
The road surface classification label is simply a binary label indicating the condition of the road surface across the entire scene. We provide binary labels for `wetness` and `snow_coverage.`
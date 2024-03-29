---
permalink: /annotations/
title:  "Annotations"
categories: jekyll update
layout: splash
---
<br>

# Annotations
On this page, we provide detailed information about the annotations that are included in our dataset. Our annotations are created by highly skilled human annotators using commercial labeling tools and have undergone a rigorous quality control process to ensure their accuracy and consistency.

We supply annotations for `Objects`, `Lanes`, `Traffic Signs`, `Ego Road`, and `Road Surface`, all of which are described in detail below. Note that the annotations can be easily read by using the development kit (`pip install zod`) found [here](https://github.com/zenseact/zod).

## Objects
Objects refer to static and dynamic objects **visible in the image**. These objects are annotated with a tightly fitting 2D bounding box indicated by the pixel coordinates of its four outermost points. If the object is also present in the point cloud (range up to `245m`), the object is also annotated with a 9-DOF 3D bounding box described by the 3D-center (`x`, `y`, `z`), the 3D dimensions (`l`, `w`, `h`), and the 3D orientation quaternion (`qw`, `qx`, `qy`, `qz`).

The dynamic objects are categorized into 4 top-level classes, namely `Vehicle`, `VulnereableVehicle`, `Pedestrian`, and `Animal`. These are then further divided into 16 sub-classes, see below for a complete list. Similarly, the static objects are divided into 6 top-level classes, namely `TrafficSign`, `TrafficSignal`, `TrafficGuide`, `PoleObject`, `TrafficBeacon`, and `DynamicBarrier`. These are then further divided into 13 sub-classes, see the below for a complete list. Moreover, the `TrafficSign` class is further divided into 156 granular classes (see the [Traffic Sign](#traffic-sign) section for more details), making it the largest commercial dataset for traffic sign annotations to date.

### Object properties

| Property | Description |
|----------|-------------|
|`unclear`| This property can be set to `True` if the annotator is unsure or if we want to discard a certain area of the image. This could be if e.g., It is in some way unclear to the human eye whether or not there is an object, e.g due to the object being too small or the image being too unsharp or blurred; It is unclear whether it is a single object or if there are more than one; Several highly overlapping objects are indistinguishable in the sense that it is practically impossible to individually mark the objects; Groups of overlapping non-pedestrian objects that are **not on Ego Road** (bicycle racks with lots of bikes, distant cars on a parking lot, groups of shopping carts, herds of farm animals, etc.,)|
| `occlusion_ratio` | Estimate how much of the object that is occluded by something in the active field of view of the camera in the image, excluding any parts of the ego vehicle body and camera housing, according to the following ranges: `None`: 0%, `Light`: 1% - 20%, `Medium`: 21% - 50%, `Heavy`: 51% - 80%, `VeryHeavy`: 81% - 100%. Being seen through the windows of another vehicle does not constitute occlusion. If an object is fully seen through another vehicle’s windows it should have occlusion level `None`|
|`relative_position`| Estimate where the object is relative the ego vehicle. Note that left and right is relative to the ego vehicle driving direction. `BeyondLeftLane`, `LeftLane`, `LeftLane_Parked`, `LeftAndEgoLane_MainlyLeft`, `LeftAndEgoLane_MainlyEgo`, `EgoLane`, `RightAndEgoLane_MainlyRight`, `RightAndEgoLane_MainlyEgo`, `RightLane`, `RightLane_Parked`, `BeyondRightLane`, `LeftLaneOncoming`, `RightLaneOncoming`, `NotOnEgoRoad`, `Inconclusive`|
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

## Lanes
This annotation task is made up of two subtasks: lane marking and road painting. This is an image-level annotation, i.e., it only conveys information in 2D. The two subtasks are described in the following sections.

### Lane markings

| Class | Instance annotation | Comment |
|-------|---------------------|---------|
|`lm_solid` | Yes | Defined as a continuous line of paint on the road separating individual lanes from each other or the road edges. They can vary in width and are usually between 10 and 30 cm wide|
|`lm_dashed` | Yes | Defined as repeating strips of paint on the road separating individual lanes from each other or the road edges. They can vary in width, length and frequency.|
|`lm_botts_dot` | Yes | Raised pavement markers used to mark lanes on highways and arterial roads. They provide tactile and auditory feedback to drivers when moving across designated travel lanes and are analogous to rumble strips. Botts' dots are most commonly white but can vary depending on local traffic rules.|
|`lm_shaded`| No | The painted markings associated to a lane marking splitting or merging should be marked with the class `shaded_area` . This includes the painted area from where the lane marking first splits, to where there are two distinct lane markings. Painted markings between the split-up lane markings that emphasize the split should also be marked `shaded_area`. This class is further split into `Split`, `Merge`, `Undefined`.|

|Property| Comment |
|-----------------|-------------|
|`MultipleLanes`| **Not applicable to `lm_shaded`**. If there are two lane markings that are right next to each other, we say that each individual lane is `Double` . If there are three or more lane markings in width, this property should be set to `Triple` or `MoreThanThree` respectively. Lane markings that are not directly adjacent to any other lane marking should have this property set to `Single`.|
|`InstanceID`| An instance is defined as one or several lane marking polygons that are connected. Typically they form a line in the image but sometimes the connection is only through context. An instance can therefore consist of one or multiple polygons, and is defined by a unique `InstanceID`. Dashed lane marking polygons that are connected in the world have the same InstanceID, for example. So the general way of thinking is that lane markings that are connected semantically in the scene belong to the same instance, where each instance have its unique `InstanceID`. It should be considered a new instance if any of the following are met|
`ShadedAreaType`| **Only the `lm_shaded` class.** The type of the shaded area. Possible values are: `Split`, `Merge`, `Undefined`, where `Undefined` is the default case.|
|`Colour`| The color of the lane marking polygon. Possible values are: `White`, `Yellow`, `Orange`, `Red`, `Blue`, `Green`, or `Other`, where `White` is the default case.|

The `InstanceID` property should be different between two instances if any of the following are met:
- A lane marking is splitting into multiple lane markings. It can be that the lane marking paint creates a split or that it splits by context. A split also occurs when a new lane is formed, even if it does not split the actual lane marking itself
- Multiple lane markings are merging into fewer lane markings. It can be that the lane marking paint is merging or a merge by context
- A lane marking changes `Colour`. An instance can only consist of one color. Meaning two partly overlapping lane markings of different colors should be two instances
- A lane marking changes from `Single` to multiple ( `Double` etc., see the `MultipleLanes` property), and there is a gap in the transition. However, if one of the single lane markings is connected to one of the multiple lane markings, the connected lane marking should belong to the same instance.
- There is a distinct gap between lane markings, for example, if there is a refuge island between two lane markings.

### Road paintings
Road paintings are roughly defined as all forms of permanent paintings on roads that are not lane markings. Lane
markings are all paintings on roads with the primary purpose to convey information about the lane extension and whether a vehicle is allowed to pass from one lane to the other. Explicitly included in the category of road paintings are shown in the table below.

| Class | Comment |
|-----------------|-------------|
|`ContainsArrow` | Whether the road painting contains an arrow as it is usually used on lanes to indicate directions. This should not be set to `True` for tiny arrows that are part of pictograms but may be set to `True` e.g. for a road painting that only contains a lane direction arrow or e.g. for a solid square containing such an arrow. One polygon is expected per arrow.|
|`ContainsPictogram` | Whether the road painting contains a pictogram, e.g. a stylized bicycle or pedestrian. The whole pictogram is expected to be marked by one polygon unless the pictogram clearly consists of multiple classes.|
|`ContainsText` | Whether the road painting contains text and/or numbers. One polygon is expected per word or (multi-digit) number|
|`ContainsTrafficSign` | Whether the road painting contains a traffic sign, e.g., a speed limit drawn on the road.  One polygon is expected per traffic sign.|
|`ContainsCrossWalk`| Whether the road painting contains a part of a cross-walk. One polygon is expected per distinct fragment of the line(s). E.g. for dashed lines, one polygon per rectangle|
|`ContainsMarker` | Whether the road painting contains a marker like stop lines, bus or lane delimiters, delimiters for give-away (almost any vertical lane marking). One polygon is expected per marker.|
|`ContainsOther`|Whether the road painting contains a class that is not one of the standard classes but should still be considered a road painting.|



## Traffic signs
![Traffic sign examples](/assets/images/traffic_signs.jpg){: .align-right width="25%" }
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
The ego road annotations refer to polygons in the image that describe the road surface on which the ego vehicle is traveling. It is divided into two classes: `Road` and `Debris` as shown in the table below.s

|Class| Comment |
|-----|---------|
|`Road`|The ego road annotations contain polygons that describe the road surface on which the ego vehicle is travelling, including roads that are connected by splits, merges, entrances and exits to this road, entrances/exits on highways and to parking lots, but not the parking lot itself, unless the Ego Car is in the parking lot. Speed bumps and other road infrastructure meant to be driven over should also be annotated as ego road. Roads of oncoming traffic separated by a barrier and other roads not connected to the ego vehicles road should not be annotated.|
|`Debris`|Debris class covers any rigid body objects larger than 15x15x15 cm located on an ego road, which are foreign to the normal roadway environment and pose danger to vehicles (the ego vehicle and vehicles on other lanes) hence interfere with normal driving. There is no upper limit of the size of a debris. Smaller objects and soft objects (like plastic bags, cups, paper etc.) do not count as debris. Objects which are parts of permanent road infrastructure (e.g. permanent bollards separating lanes or speed bumps are not Debris )|


## Road surface
The road surface classification label is simply a binary label indicating the condition of the road surface across the entire scene. We provide binary labels for `wetness` and `snow_coverage.`
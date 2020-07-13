# OpenHDMap
This is an open source HD map project for autonomous driving. The precision map production process is divided into four parts: **map collection, map production, map labeling, and map saving**. This project mainly uses lidar as a collection sensor to provide the map making process.  

The goal is to provide a complete mapping process for autonomous driving systems and simulation.  

If you have any advice, please feel free to contact us.  

## Introduce  
Let ’s start with how to make an HD map. The HD map making process can be divided into 4 steps. 
1. Map collection  
2. Map production  
3. Map labeling  
4. Map saving  

Next we introduce these four processes respectively.  
![HDmap_pipeline](docs/img/hdmap_pipeline.jpg)  

#### 1. Map collection
First, we use a map collection car equipped with lidar, camera, GPS and IMU to collect maps. The data currently used is an open source dataset. We plan to provide recommended hardware and toy cars later.  

You can use the collected data set or equip your own sensors to collect data.    
* Collected dataset: KITTI  
* Recommended equipment: todo (If you have good suggestions, welcome to recommend)  

#### 2. Map production
Then, We need to generate street and building models based on the collected point cloud data. The production process is the stitching of point clouds. This process is often referred to as point cloud registration. After stitching the point clouds frame by frame, a three-dimensional model of the entire street is obtained. You scanned the whole earth with lidar. it looks really cool, right?  

There are currently two methods to generate point cloud maps, one is through NDT Mapping, and the other is offline SLAM mapping. At present, we choose to use NDT Mapping. Here we refer to the implementation of autoware.  

There are several SLAM mapping methods to refer to:  
* LOAM
* Cartographer
* hdl_graph_slam
* blam
* A-LOAM
* LeGO-LOAM
* LIO-mapping
* interactive_slam

> We will use the above method to build the map later.

#### 3. Map labeling
After you have completed the 3D model of the map, this part of the map is called a point cloud map. To get lane line, traffic lights and traffic sign information, we also need to label the map. At present, labeling is mainly done manually. We will provide labeling tools. The labeled map is called HD map.  

The two most important questions in map labels are as follows.  
* **Sensor fusion** - Because the resolution of the point cloud is not high, the purpose of sensor fusion is to map the pictures of the camera to the point cloud to improve the resolution of lane lines and traffic signs.  
* **Automatic labeling** - Automatic labeling capability for large-scale map production and maintenance.  

At present, we adopt the method of manual annotation, and we will gradually solve the above two problems later.  


#### 4. Map saving
The preservation of HD maps is divided into two parts, one is the format of the map, and the other is the layers of the map.
* Map format   
The format of the map is currently opendrive. In short, the project hopes to have a unified labeling format.  

- Map layers    
Map is divided into 3 layers: base layer, positioning layer and dynamic layer.
    - Base layer. The basic layer is the structured information of the map generated by the above annotations, including lane lines, traffic rule information, etc.  
    - Positioning layer. The positioning layer is some original point clouds that are helpful for autonomous driving positioning, such as telephone poles, traffic signs, buildings, etc.  
    - Dynamic layer. The dynamic layer publishes some dynamically changing information, such as traffic conditions, traffic accidents ahead, etc.

We currently use Apollo HD map format to work with simulator to verify HD maps.  

## Quick start

#### Introduction
```
.
├── docs             // documents
├── map_format       // Implement map format conversion function
├── map_label_tool   // Map labeling tool
├── map_production   // Create high-precision map which use to label
```

#### 1. Map production
We use "Autoware NDT Mapping" to build a small map from open dataset. The code is reference in "core_perception/lidar_localizer/nodes/ndt_mapping" [Link](https://gitlab.com/autowarefoundation/autoware.ai/core_perception). The code is now in dir "map_production".  

#### 2. Map labeling
We will soon release a map annotation tool, which will in "map_label_tool" dir.  

#### 3. Map format
After labelling semantic maps, we provide multiple map formats to different open source projects like Apollo and autoware.  

#### 4. End-to-end pipeline


## Examples  

## Benchmark  
Benchmark of the process:  
* accurate
* time

## Reference
[vector tiles](https://docs.mapbox.com/vector-tiles/reference/)  
[awesome-vector-tiles](https://github.com/mapbox/awesome-vector-tiles)  
[paperjs](http://paperjs.org/examples/hit-testing/)  
[best-javascript-drawing-libraries](https://www.slant.co/topics/28/~best-javascript-drawing-libraries)  


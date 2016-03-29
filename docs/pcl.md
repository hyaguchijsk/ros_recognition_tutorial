# How to use PCL

## How to convert from ROS msg to PCL Point Cloud

ROSでPCL関連のパッケージは[perception_pcl]に集まっています．
[Tutorials]に簡単な使い方が記載されていますが，
ここでは型に注目してください．

ROSでは点群は`sensor_msgs/PointCloud2`型になっていますが，
PCLで点群の処理を行うためには`pcl::PointCloud`型である必要があります．
このための相互変換には，
`pcl::fromROSMsg`,`pcl::toROSMsg`を使います．

## How to analyze Point Cloud format

`sensor_msgs/PointCloud2`型から点群の素性を探るためには，
`width`,`height`,`fields`を見てみましょう．
前２つはそのままですが，次の`fields`は事前に調べておくと有用です．
その点群がどのような情報を持っているかを調べられます．

例えば，ps4eyeの点群の`fields`を調べてみましょう．

```
rostopic echo /stereo/points2/fields
```

とすると，以下のような情報が得られます．

```
-
  name: x
  offset: 0
  datatype: 7
  count: 1
-
  name: y
  offset: 4
  datatype: 7
  count: 1
-
  name: z
  offset: 8
  datatype: 7
  count: 1
-
  name: rgb
  offset: 16
  datatype: 7
  count: 1
---
```

これは，ps4eyeの点群が`x,y,z`の位置情報と，
`rgb`の色情報を持っていることを表しています．
[Common PointCloud2 field names]に種類が記載されていますが，
この他にも点群は法線情報`normal_{x,y,z}`などを持つことができます．


[perception_pcl]: http://wiki.ros.org/perception_pcl
[Tutorials]: http://wiki.ros.org/perception_pcl/Tutorials
[Common PointCloud2 field names]: http://wiki.ros.org/pcl/Overview#Common_PointCloud2_field_names

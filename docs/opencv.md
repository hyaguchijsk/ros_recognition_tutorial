# How to use OpenCV

## ROS OpenCV Samples

[opencv_apps]にOpenCVを使ったROSパッケージのサンプルがあります．

## image_transport and cv_bridge

`Image`型を取り扱うためには[image_transport]を，
ROSのメッセージとOpenCVの型を変換するには[cv_bridge]を使います．
C++のチュートリアルは
[image_transport/Tutorials]
と
[Converting between ROS images and OpenCV images (C++)]
に詳細記述があります．

## Camera Parameters

カメラパラメータは`camera_info`を参照することで得られます．

```
rostopic echo {camera_name}/camera_info
```

として，以下のような出力が得られます．（この例はps4eyeを使用しています．）

```
header:
  seq: 3402
  stamp:
    secs: 1459228129
    nsecs: 655101027
  frame_id: /ps4eye_frame
height: 400
width: 640
distortion_model: plumb_bob
D: [-0.001645, -0.002527, 0.000978, 0.001781, 0.0]
K: [425.075706, 0.0, 321.26391, 0.0, 424.860727, 196.440802, 0.0, 0.0, 1.0]
R: [0.999992, -0.001109, 0.003743, 0.001097, 0.999994, 0.003196, -0.003747, -0.003192, 0.999988]
P: [428.591565, 0.0, 316.849155, 0.0, 0.0, 428.591565, 196.532789, 0.0, 0.0, 0.0, 1.0, 0.0]
binning_x: 0
binning_y: 0
roi:
  x_offset: 0
  y_offset: 0
  height: 0
  width: 0
  do_rectify: True
```

ここで有用な情報は`width`,`height`,そして`P`です．
`P`はProjection Matrixを表し，
`P[0]`はx軸方向の焦点距離，`P[2]`はx軸における中心座標，
`P[5]`はy軸方向の焦点距離，`P[6]`はy軸における中心座標，
をそれぞれ表しています．単位は全てピクセルです．

（ちなみにこれは左目側で，右目側`P[3]`にはベースライン距離が入ります．）


## How to synchronize image and camera_info

`image`と`camera_info`は対になって扱われる必要があるため，
時刻同期をとって，単一のサブスクライバ内で扱えると便利です．
このための機能が[message_filters]に用意されています．

### CameraSubscriber

`image_transport::CameraSubscriber`が一番簡単に記述できる方法です．

```
void ImageCallback(
  const sensor_msgs::ImageConstPtr& image_msg,
  const sensor_msgs::CameraInfoConstPtr& info_msg) {
  // do something;
}
```

を宣言しておき，

```
ros::NodeHandle handle;
image_transport::ImageTransport it(handle);

image_transport::CameraSubscriber sub_camera_ =
  it_.subscribeCamera("image", 1, ImageCallback);
```

とすることで，同期された２つのメッセージを扱うことができます．



[opencv_apps]: http://wiki.ros.org/opencv_apps
[image_transport]: http://wiki.ros.org/image_transport
[cv_bridge]: http://wiki.ros.org/cv_bridge
[image_transport/Tutorials]: http://wiki.ros.org/image_transport/Tutorials
[Converting between ROS images and OpenCV images (C++)]: http://wiki.ros.org/cv_bridge/Tutorials/UsingCvBridgeToConvertBetweenROSImagesAndOpenCVImages
[message_filters]: http://wiki.ros.org/message_filters

# How to use camera

## Introduction

ここではカメラの使い方について説明します．

## Camera

通常のWebカメラの場合，
UVCと呼ばれる規格に対応したものであればすべて同じように使うことができます．
GigEカメラなどドライバが必要なカメラの場合，
別途専用ノードを用意する必要があります．

カメラ画像の出力は，
`sensor_msgs/Image`型の画像と，
`sensor_msgs/CameraInfo`型のカメラパラメータの２つとなり，
この２つが組になっていないとうまく動作しません．


## 3D camera

ここでは三次元情報を計測可能なカメラを三次元カメラと呼びます．
三次元カメラでは三次元点群が出力されます．
カラーカメラを持ったものでは画像が合わせて出力されるか，
もしくは三次元点群に色情報が追加されます．

三次元点群は
`sensor_msgs/PointCloud2`型のメッセージとして出力されます．
これを実際にプログラムで扱うためには`PCL`の点群型に変換して使うのが一般的です．

三次元カメラには
２つのカメラを並べてその見え方の差を元に計測を行うステレオカメラ，
赤外線プロジェクタを用いたパターンを投影して距離を計測するカメラ，
レーザーの反射にかかる時間を元に距離を計測するToF方式カメラなど，
様々な原理のカメラが存在します．
その中でもよく使われるものを紹介します．

### Kinect, Xtion Pro Live

KinectやXtionは赤外線パターン投光方式の三次元カメラです．
`openni2_launch`を使いましょう．

```
roslaunch openni2_launch openni2.launch depth_registration:=true
```

カラー画像は`/camera/rgb/image_raw`に，
三次元点群は`/camera/depth_registered/points`に出力されます．

### Kinect2

TBD

### PlayStation Camera (ps4eye)

PlayStation Cameraはステレオカメラです．
`ps4eye`というパッケージを使います．

```
roslaunch ps4eye stereo.launch
```

カラー画像は
`/stereo/left/image_rect_color`と
`/stereo/right/image_rect_color`に，
三次元点群は`/stereo/points2`に出力されます．


## How to visualize

カメラ画像の場合，`image_view`を使って画像の内容を見ることができます．

三次元点群の場合は`rviz`を使いましょう．


## Camera calibration

### Monocular camera

### Stereo camera

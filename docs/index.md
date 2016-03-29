# ROS Recognition tutorial

## About

このドキュメントでは，ROSを用いた認識機能の開発の初歩について解説します．
ROSの基本的な使い方を習得し，
OpenCV,PCLをROSで使っていこうという中級者向けです．

このドキュメントの内容は
ROSがインストールされていることが前提となります．
[ROS/Installation]を参考にインストールしてください．

また，[wstool],[catkin-tools]もあわせてインストールすると便利です．

```bash
sudo apt-get install python-wstool python-catkin-tools
```

インストール終了後，catkinのワークスペースを作ってください．
例えば以下のようにします．

```bash
mkdir ~/catkin_ws
cd ~/catkin_ws
wstool init src
catkin init
catkin build
source ~/catkin_ws/devel/setup.bash
```

[ROS/Installation]: http://wiki.ros.org/ROS/Installation
[wstool]: http://wiki.ros.org/wstool
[catkin-tools]: https://catkin-tools.readthedocs.org/en/latest/

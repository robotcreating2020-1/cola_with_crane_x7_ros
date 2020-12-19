# cola_with_crane_x7_ros  

## 実装内容  
  
[crane_x7](https://rt-net.jp/products/crane-x7/)を用いてコーラを振るサンプルコードです。  
crane_x7とIntelRealSenseを用いて実機動作を行っています。  
  
--- 
  
## 動作環境  
  
以下の環境で動作確認しています。  
- ROS Melodic  
　- OS: Ubuntu 18.04.5 LTS  
　- ROS Distribution: Melodic Morenia 1.14.3  
　- Rviz 1.13.13  
　- Gazebo 9.0.0  
- [rt-net/crane_x7_ros](https://github.com/rt-net/crane_x7_ros)  
- [IntelRealSense/realsense-ros](https://github.com/IntelRealSense/realsense-ros)  
  
---
  
## 環境構築  
  
1. crane_x7_rosをインストールします。  
```sh
cd ~/catkin_ws/src  
git clone https://github.com/rt-net/crane_x7_ros.git  
```  
　詳しくは[こちら](https://github.com/rt-net/crane_x7_ros)を参照してください。  
  
1. realsense-rosをインストールします。  
　詳しくは[こちら](https://github.com/IntelRealSense/realsense-ros)を参照してください。  
　また、今回は[demura.net/Ubuntu18.04: RealSense D435iをROS Melodicで使う](https://demura.net/robot/16525.html)を参考にさせていただきました。  
  
1. 本パッケージをインストールします。  
```sh
cd ~/catkin_ws/src  
git clone https://github.com/robotcreating2020-1/cola_with_crane_x7_ros  
cd ~/catkin_ws  
catkin_make  
```  
  
---
  
## 実行方法  
  
### シミュレータを使う場合  

IntelRealSenseを用いた動作はできません。  
実機での動作を確認するために使用してください。  
  
シミュレータを使う場合、[rt-net/crane_x7_ros/crane_x7_gazebo](https://github.com/rt-net/crane_x7_ros/tree/master/crane_x7_gazebo)の[worldディレクトリ](https://github.com/rt-net/crane_x7_ros/tree/master/crane_x7_gazebo/worlds)に本パッケージ[cola_with_crane_x7_ros/crane_x7_gazebo/world]の[table3.world](https://github.com/robotcreating2020-1/cola_with_crane_x7_ros/blob/master/crane_x7_gazebo/worlds/table3.world)を追加してください。  
  
また、[rt-net/crane_x7_ros/crane_x7_gazebo](https://github.com/rt-net/crane_x7_ros/    tree/master/crane_x7_gazebo)の[launchディレクトリ](https://github.com/rt-net/crane_x7_ros/tree/master/crane_x7_gazebo/launch)の[crane_x7_with_table.launch](https://github.com/rt-net/crane_x7_ros/blob/master/crane_x7_gazebo/launch/crane_x7_with_table.launch)内の28行目を以下のように変更してください。  
  
- 変更前  
`<arg name="world_name" value="$(find crane_x7_gazebo)/worlds/table.world"/>`  
- 変更後  
`<arg name="world_name" value="$(find crane_x7_gazebo)/worlds/table3.world"/>`  
  
  
1. シミュレータを起動します。  
```sh
roslaunch crane_x7_gazebo crane_x7_with_table.launch  
```  

1. 本パッケージのサンプルコードを実行します。  
　一連の動作を確認する場合、detect_bottle.pyを実行してください。  
```sh
rosrun cola_with_crane_x7_ros detect_bottle.py
```  
その他のサンプルコードの詳細は[../cola_with_crane_x7_ros/crane_x7_example](https://github.com/robotcreating2020-1/cola_with_crane_x7_ros/tree/master/crane_x7_examples)を参照してください。
  
### 実機を使う場合  
  
1. crane_x7とボトルを以下のように配置してください。  
<img src= https://github.com/Dansato1203/images/blob/master/RobotDesign3/IMG_3795.jpg width=500px />  
<img src= https://github.com/Dansato1203/images/blob/master/RobotDesign3/%E3%83%9C%E3%83%88%E3%83%AB%E3%81%AE%E9%85%8D%E7%BD%AE%E3%82%A4%E3%83%A1%E3%83%BC%E3%82%B8.png width=500px />  

本パッケージのサンプルコードでは赤いボトルを掴みます。  
配置イメージでは右側に赤いボトルを配置していますが、3点のうちどこでも構いません。  
  
  
1. IntelRealSenseを起動します。
```sh
roslaunch realsense2_camera rs_camera.launch  
```
1. crane_x7を起動します。  
CRANE-X7の制御信号ケーブルを制御用パソコンへ接続し、以下を実行します。  
```sh
sudo chmod 666 /dev/ttyUSB0  
```  

1. 実機で動作を確認する場合、制御信号ケーブルを接続した状態で次のコードを実行します。  
```sh
roslaunch crane_x7_bringup demo.launch fake_execution:=false  
```  

1. 次に本パッケージのfind_red.pyを実行します。  
```sh
rosrun cola_with_crane_x7_ros find_red.py  
```  

1. 最後にdetect_bottle.pyを実行するとアームが動きコーラを振ります。  
```sh
rosrun cola_with_crane_x7_ros detect_bottle.py  
```

find_red.py、detect_bottle.pyの詳細は[こちら](https://github.com/robotcreating2020-1/cola_with_crane_x7_ros/tree/master/crane_x7_examples)を参照してください。  


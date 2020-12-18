# cola_with_crane_x7_ros  

## 実装内容  
  
[crane_x7](https://rt-net.jp/products/crane-x7/)を用いてコーラを振るサンプルコードです。  
crane_x7とIntelRealSenseを用いて実機動作を行っています。  
  
--- 
  
## 動作環境  
  
以下の環境で動作確認しています。  
・ROS Melodic
　・OS: Ubuntu 18.04.5 LTS
　・ROS Distribution: Melodic Morenia 1.14.3
　・Rviz 1.13.13
　・Gazebo 9.0.0  
・[rt-net/crane_x7_ros](https://github.com/rt-net/crane_x7_ros)  
・[IntelRealSense/realsense-ros](https://github.com/IntelRealSense/realsense-ros)  

## 環境構築  
  
・crane_x7_rosをインストールします。  
```sh
cd ~/catkin_ws/src  
git clone https://github.com/rt-net/crane_x7_ros.git  
```  
詳しくは[こちら](https://github.com/rt-net/crane_x7_ros)を参照してください。  
  
・realsense-rosをインストールします。  
詳しくは[こちら](https://github.com/IntelRealSense/realsense-ros)を参照してください。  
また、今回は[demura.net/Ubuntu18.04: RealSense D435iをROS Melodicで使う](https://demura.net/robot/16525.html)を参考にさせていただきました。  
  
## 実行方法  
  
・IntelRealSenseを起動します。
```sh
roslaunch realsense2_camera rs_camera.launch  
```
・crane_x7を起動します。  
CRANE-X7の制御信号ケーブルを制御用パソコンへ接続し、以下を実行します。  
```sh
sudo chmod 666 /dev/ttyUSB0  
```  

実機で動作を確認する場合、制御信号ケーブルを接続した状態で次のコードを実行します。  
```sh
roslaunch crane_x7_bringup demo.launch fake_execution:=false  
```  



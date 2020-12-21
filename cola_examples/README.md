# cola_example  
  
本パッケージはオリジナルである[rt-net/crane_x7_ros](https://github.com/rt-net/crane_x7_ros)に対し、千葉工業大学 未来ロボティクス学科で開講された講義内でのグループ robotcreating2020-1が変更を加えています。  
このパッケージには、 [Apache 2.0ライセンス](http://www.apache.org/licenses/LICENSE-2.0)で配布されている製作物が含まれています。  
  
[crane_x7](https://github.com/rt-net/crane_x7_ros)でコーラを振るときに用いるコードをまとめたサンプルコード集です。  
crane_x7_rosの他にIntelRealSense/realsense-rosを用いています。  
  
---
  
## 実装内容  
  
### bottle_drop.py
  
ボトルを緩衝材の上に落とすことを想定したコードです。  
ボトルを掴み、ボトルを寝かせ、高さ200mmから真下に落とします。
  
<img src=https://github.com/Dansato1203/images/blob/master/RobotDesign3/bottle_drop.gif width=700px/>  
  
次のコマンドで動作を実行します。  
```sh
rosrun cola_with_crane_x7_ros bottle_drop.py  
```  
  
--- 
  
### shake_mode.py

ボトルを持ち上げ、人間がボトルを振るようにアーム全体を用いて振る動作を行います。  
  
<img src=https://github.com/Dansato1203/images/blob/master/RobotDesign3/shake_mode.gif width=700px/>  
  
次のコマンドで動作を実行します。  
```sh
rosrun cola_with_crane_x7_ros shake_mode.py  
```  
  
---  
  
### looking_bottle.py  
  
3色のボトルが決められた位置にあることを想定し、realsenseにボトルを見せに行く動作を行います。  
  
<img src=https://github.com/Dansato1203/images/blob/master/RobotDesign3/looking_bottle.gif width=700px/>  
  
次のコマンドで動作を実行します。  
```sh
rosrun cola_with_crane_x7_ros looking_bottle.py  
```  
  
---
  
### find_red.py  

赤色を検出するプログラムです。  
[IntelRealSense/realsense-ros](https://github.com/IntelRealSense/realsense-ros)を用いています。  
realsenseからカラー画像をsubscribeし、imgmsg_to_cv2を用いてROSからOpencvの形式に変換しています。  

subscribeしたカラー画像から赤色成分を抽出し、その輪郭を矩形で囲っています。  
また、検知した赤色成分の輪郭の矩形の面積を/bottle_sizeというトピックにpublishしています。  
このサンプルコードでは赤色ボトル以外の赤色成分の誤検出を防ぐため、矩形の面積が10000以上のときのみpublishしています。  
面積が一定(サンプルの場合10000)以上の赤い物体が検出できない場合は特に何も行いません。  

<img src=https://github.com/Dansato1203/images/blob/master/RobotDesign3/IMG_3711.PNG width = 700px/>  
上記の画像は実際に赤い物体を検出し、輪郭を矩形で囲ったサンプル画像になります。  
  
次のコマンドで動作を実行します。  
```sh
rosrun cola_with_crane_x7_ros find_red.py  
```  


--- 
  
### detect_bottle.py
  
上記のbottle_drop.py, shake_mode.py, lookng_bottle.pyを統合し、掴んだボトルをもとの位置に戻す動作を追加したコードです。  
find_red.pyを実行した状態で実行することで、3つの位置のボトルから赤いボトルを検出し、赤いボトルを振ることができます。  
  
<img src=https://github.com/Dansato1203/images/blob/master/RobotDesign3/detect_bottle.gif width=700px/>  
  
次のコマンドで動作を実行します。  
```sh
rosrun cola_with_crane_x7_ros detect_bottle.py  
```  


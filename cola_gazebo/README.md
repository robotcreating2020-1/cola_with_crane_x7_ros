# cola_gazebo  
  
本パッケージはオリジナルである[rt-net/crane_x7_ros](https://github.com/rt-net/crane_x7_ros)対し、千葉工業大学 未来ロボティクス学科で開講された講義内でのグループ robotcreating2020-1が変更を加えています。
このパッケージには、 [Apache 2.0ライセンス](http://www.apache.org/licenses/LICENSE-2.0)で配布されている製作物が含まれています。

  
---
  
## オリジナルからの変更点  
  
1. worldsフォルダ内にtable3.worldというworldファイルを追加しています。  
table3.worldには、机の上に径が50mm, 高さが200mmのボトルを3本を追加しています。  
<img src=https://github.com/Dansato1203/images/blob/master/RobotDesign3/IMG_3815.PNG width=500px/>  
  
2. launchファイルの一部を[オリジナル](https://github.com/rt-net/crane_x7_ros/blob/master/crane_x7_gazebo/launch/crane_x7_with_table.launch)から変更しています。  
  
　具体的な変更箇所は、crane_x7_with_table.launch内の28行目を  
  
- 変更前  
`<arg name="world_name" value="$(find crane_x7_gazebo)/worlds/table.world"/>`  
- 変更後  
`<arg name="world_name" value="$(find crane_x7_gazebo)/worlds/table3.world"/>`  
  
のように変更しています。  


# 方狗科技樹

  * [CD-05B 方犬](https://github.com/SphericalCowww/ROS_leggedRobot_testBed): 測試機 <img src="https://github.com/SphericalCowww/ROS_leggedRobot_testBed/blob/main/CubicDogo.png" width="100">

  * [CD-06B 方狗](https://github.com/SphericalCowww/CubicDoggo): 原型機 <img src="https://github.com/SphericalCowww/ROS_Cubic_Doggo/blob/main/CubicDoggo2.png" height="100"> 
    -  [CD-06R 高機動方狗](https://github.com/SphericalCowww/CubicDoggo_06R): 結構強化，加裝 IMU 慣性測量單元 <img src="https://github.com/SphericalCowww/CubicDoggo_06R/blob/main/CubicDoggo2.png" height="100"> 
    -  [CD-06Z 精神感應方狗](https://github.com/SphericalCowww/CubicDoggo_06Z): 物理模擬，強化學習 <img src="https://github.com/SphericalCowww/CubicDoggo_06Z/blob/main/fig_MuJoCo.webp" height="100">
  * [CD-07B 方狗夫](https://github.com/SphericalCowww/CubicDoggo_07B): 採用高扭力、低成本的伺服馬達 <img src="https://github.com/SphericalCowww/CubicDoggo_07B/blob/main/fig_Wouf0.png" height="100">
    - [CD-07R-35 高機動方狗夫](https://github.com/SphericalCowww/CubicDoggo_07R-35): 步態優化，加裝 IMU 慣性測量單元
    - CD-07B-3 特裝型方狗夫: 加裝光達，攝像機，和麥克風
    - CD-N01 精神感應方狗夫: 物理模擬，強化學習
  * CD-09B 方狗姆: 加裝輪胎
    - CD-09R 里克方狗姆: 輪腳共驅，光達導航
  * [CD-14A 方狗古](https://github.com/SphericalCowww/CubicDoggo_14A): 加裝機械臂，[機甲奪旗賽](https://github.com/SphericalCowww/tag_of_flag)專用
    - CD-14B 高機動方狗古: 機械臂結構和控制優化，加裝 IMU 慣性測量單元
    - CD-N02 方狗克: 臂腳物理模擬，強化學習
  * CD-Y15 方狗甘恩
  * CD-AN03 方狗布勞: 大型語言模型決策樹
    - CD-AN08 方狗艾爾: 加載懸停無人機

# Cubic Doggo Tech Tree Chronicle

  * [CD-05B Cubic Dogo](https://github.com/SphericalCowww/ROS_leggedRobot_testBed): creation stage <img src="https://github.com/SphericalCowww/ROS_leggedRobot_testBed/blob/main/CubicDogo.png" width="100">
  * [CD-06B Cubic Doggo](https://github.com/SphericalCowww/CubicDoggo): reference machine <img src="https://github.com/SphericalCowww/ROS_Cubic_Doggo/blob/main/CubicDoggo2.png" height="100"> 
    -  [CD-06R Doggo High Mobility](https://github.com/SphericalCowww/CubicDoggo_06R): mechanical improvements and with IMU <img src="https://github.com/SphericalCowww/CubicDoggo_06R/blob/main/CubicDoggo2.png" height="100"> 
    -  [CD-06Z Doggo Neucommu](https://github.com/SphericalCowww/CubicDoggo_06Z): with simulation (Gazebo/MuJoCo) and reinforcement learning (PyTorch) <img src="https://github.com/SphericalCowww/CubicDoggo_06Z/blob/main/fig_MuJoCo.webp" height="100">
  * [CD-07B Cubic Wouf](https://github.com/SphericalCowww/CubicDoggo_07B): with stronger and cheaper servos <img src="https://github.com/SphericalCowww/CubicDoggo_07B/blob/main/fig_Wouf0.png" height="100">
    - [CD-07R-35 Wouf High IMUbility](https://github.com/SphericalCowww/CubicDoggo_07R-35): gait optimization and with IMU
    - CD-07B-3 Wouf Custom: with LIDAR, camera, and microphone
    - CD-N01 Isaac Neucommu: with simulation (Isaac Sim) and reinforcement learning (Isaac Lab)
  * CD-09B Dogm: with wheels
    - CD-09R Rick Dogm: wheel-leg coordination, and with LiDAR and ROS2 Nav2
  * [CD-14A Googboi](https://github.com/SphericalCowww/CubicDoggo_14A): with SO-101 arm, designed for the [Tag of Flag](https://github.com/SphericalCowww/tag_of_flag) game
    - CD-14B Goog Zoomie Mobility: arm optimization and with IMU
    - CD-N02 Doggg: arm-leg coordination with RL
  * CD-Y15 Gyanine
  * CD-AN03 Brawboi: LLM decision tree, https://github.com/Sollimann/bonsai
    - CD-AN08 Elmutt: LLM and with drone hovering on the top: https://ts2.store/en/11643-ryze-tello-educational-drone.html?ts2_country=DE&ts2_currency=EUR

## Servo comparison considerations

  * Torque density: Nm/kg of actuator
  * Static torque margin: Available torque minus torque required to support the robot
  * Dynamic torque reserve: Available torque beyond the requirements of the intended gait and disturbances

For larger robots, the dynamic torque reserve matters more, so BLDC is the go-to choice. For smaller robots, torque density and static torque margin matter more, so serial-bus or PWM servos make more sense. To have position/velicity feedback for closed-loop reinforcement training, the serial-bus servos will be the final choice

## Regarding grip on the feet

  * It will enable a faster walking gait and reduce vertical force when carrying payload
  * It, however, adds significant complication in requiring precise foot positioning by the gait algorithm. For instance, the standing-up sequence cannot just let the feet slide into position, but must lift and place them in position. Every operation requires lifting the legs
  * Doing the precise footing wrong with high grip will sharply increase vertical forces against the servos, causing a sort of implosion of the robot's legs
  * Having tested no-grip walking on a smooth surface versus on a carpet, the walk gait is not all of a sudden better on the carpet because of the increase in grip. The walk gait smoothness is more a matter of robot body balancing than about adding grip to the feet



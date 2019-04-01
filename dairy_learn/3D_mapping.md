#Google cartographer + Velodyne 仿真

1.安装好cartographer


2.启动demo演示，正常可以看到rviz启动并开始建图
2d:
roslaunch cartographer_ros demo_backpack_2d.launch  bag_filename:=/home/hitnuc/catkin_lidar/src/cartographer_ros/bag/cartographer_paper_deutsches_museum.bag

3.保存地图，结束测试

1、先调用服务来关闭传感器数据的接收
rosservice call /finish_trajectory 0

2、将当前地图信息的快照保存为后缀名为.pbstream
rosservice call /write_state "{filename: '${HOME}/Downloads/mymap.pbstream'}"

filename可以根据自己的需要更改。

3、将后缀名为.pbstream的地图信息，转化成ros地图信息
rosrun cartographer_ros cartographer_pbstream_to_ros_map -map_filestem=/home/kk/Downloads/mymap -pbstream_filename=/home/kk/Downloads/mymap.pbstream -resolution=0.05

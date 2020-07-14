# PCL与ROS之间的数据转换

## 1.PointCloud与sensor_msgs::LaserScan的转换
* 
## 2.pcl::PointCloud::Ptr 和Pcl::PointCloud两个类的相互转换  [参考](https://blog.csdn.net/parker_1/article/details/99342637)
* Ptr类型和非Ptr类型相互转换  
```
pcl::PointCloud<pcl::PointXYZ>::Ptr cloud_Ptr(new pcl::PointCloud<pcl::PointXYZ>);  
pcl::PointCloud<pcl::PointXYZ> cloud;   
cloud=*cloud_Ptr;  
cloud_Ptr=cloud.makeShared;  
```

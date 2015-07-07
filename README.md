#** 高德地图的使用方法(参照高德地图开发者文档): **#
##1.进入项目，touch podfile 
	platform :ios, '8.0' #手机的操作系统 
	pod 'AMap3DMap'
	\#pod 'AMap2DMap'
	\#pod 'AMap3DMap', '2.4.0'
	\#退回原来老的版本'2.4.0'
  	\#两个中选择一个，不能同时使用
	pod 'AMapSerch' 

pod install
open the project (xcworkingspace)##

2.create Swift-Bridging-Header.h file
Build Settings -> Swift Compiler - code Generation ->Objective-C Bridging Header(...Swift-Bridging-Header.h)
3.apply for apiKey.

4.display the map

let apiKey  = ""
class ViewController:UIViewController,MAMapViewDelegate
var mapView:MAMapView? 

MAMapServices.sharedServices().apiKey = apiKey
mapView = MAMapView(frame:self.view.bounds);mapView!.delegate = self;self.view.addSubview(mapView!)
5.逆地理编码查询

逆地理编码是高德提供的众多服务中的一种，被广泛用于iOS的LBS应用。实现逆地理编码查询功能需要搜索SDK（AMapSearchKit.framework）。

搜索SDK提供的服务功能的实现步骤有以下四点：

（1） 初始化主搜索对象AMapSearchAPI，并继承搜索协议 AMapSearchDelegate 。

（2） 构造 Request 对象，配置搜索参数。

（3） 通过主搜索对象以 Request 对象为参数，发起搜索。

（4） 实现搜索协议中对应的回调函数，通过解析 Response 对象获取搜索结果。

这里通过定位获取当前位置的经纬度，在点击定位标注（小蓝点）时，进行逆地理编码，在弹出的气泡中显示定位点的地址。实现该场景有以下几个步骤：

1.开启定位，显示定位标注（小蓝点）。

2.在定位的回调函数中获取定位点的经纬度。

3.点击定位标注，执行逆地理编码查询。

4.在逆地理编码回调中设置定位标注的title和subtitle。

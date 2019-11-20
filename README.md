# kriging-contour
对离散点进行克里金插值并输出矢量等值面

安装
```
git clone git@github.com:FreeGIS/kriging-contour.git
cd kriging-contour
npm install
```
编译
```
npm run pretest
```


使用说明：freegis.kriging_contour(dataset,weight_field,kriging_params,weight_breaks);
```
dataset：geojson格式的featureclass数据集，feature是图形是点
weight_field：绑定权重字段名称
kriging_params：克里金插值参数
weight_breaks：权重生成等值面分级数组
```
示例代码：
```
	//计算克里金等值面
		let kriging_contours=freegis.kriging_contour(dataset,'level',{
			model:'exponential',
			sigma2:0,
			alpha:100
		},[0,10,20,30,40,50,60,70,80,90,100]);
 ```
kriging-contour是基于[kriging.js](https://github.com/oeo4b/kriging.js)修改的，原kriging.js中plot方法，将插值结果grid转换渲染到canvas，放大后等值面锯齿状严重，本修改结合d3_contour.js重新实现
其转换方法，将grid转换成等值面的矢量geojson格式，前端地图api解析即可绘制，使用上也更方便点，无需非gis专业开发者进行像素与地理坐标转换换算。
kriging.js渲染效果:
![kriging.js渲染效果](https://github.com/FreeGIS/kriging-contour/blob/master/doc/raster.jpg)
kriging-contour渲染效果:
![kriging-contour渲染效果](https://github.com/FreeGIS/kriging-contour/blob/master/doc/vector.jpg)

BUG
因笔者精力有限，目前该项目存在bug，即多次刷新页面，部分时候生成的结果如下图：
偶尔出现的bug效果:
![偶尔出现的bug效果](https://github.com/FreeGIS/kriging-contour/blob/master/doc/bug.png)
希望有同仁能有时间修改并提交仓库合并。

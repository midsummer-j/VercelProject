### 修改测距测面时默认样式

- 版本：`@arcgis/core": "^4.18.1`
- 引用：`import Measurement from "@arcgis/core/widgets/Measurement";`

```
loadView() {
  MapManager.mapView.ui.add(this.measurement, "top-right");
  // Set the views for the widgets
  this.measurement.view = MapManager.mapView;
},
measurementInit() {
  const that = this;
  that.measurement.watch("activeWidget", function(evt) {
    //如果需要修改3D测量样式，判断当前的地图模式，打印相应控制板palette
    if (evt !== null) {
      if (that.measurement.activeTool === "distance") {
        evt.viewModel.palette.handleColor = [62, 138, 212, 0.5];
        evt.viewModel.palette.pathPrimaryColor = [62, 138, 212, 255];//原样式为斑马线，设置pathPrimaryColor和pathSecondaryColor相同即可为纯色
        evt.viewModel.palette.pathSecondaryColor = [62, 138, 212, 255];
        evt.viewModel.unit = "meters";//修改默认单位
        evt.viewModel.unitOptions = ["meters", "kilometers"];//修改默认单位可选项
      } else {
        evt.viewModel.palette.fillColor = [62, 138, 212, 0.3];
        evt.viewModel.palette.handleColor = [62, 138, 212, 0.5];
        evt.viewModel.palette.pathColor = [62, 138, 212, 0.8];
        evt.viewModel.unit = "square-meters";//修改默认单位
        evt.viewModel.unitOptions = ["square-meters", "square-kilometers"];//修改默认单位可选项
      }
    }
  });
},
```

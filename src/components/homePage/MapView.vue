<template>
  <div id="center-map1">
    <div>
      <div
        v-show="points.length && point.markerIsShown"
        v-for="point in points"
        :key="point.id"
        :style="
          'width: 17px; height: 40px; position: absolute; z-index: 1; background: url(' +
            (point.isHighSpeed?yollow_point:green_point) +
            ');' +
            point.style
        "
        :id="point.id"
      >
        <div
          v-if="point.toolotipIsShown"
          :style="
            'width:' +
              (point.projectName.length * 13 + 55) +
              'px;padding:0px 0px 0px 18px;text-align:center;cursor:pointer;'
          "
          @click="goToTuPu(point.id)"
        >
          <div
            :style="
              'border: 1px solid ' +
                (point.isHighSpeed?yellow_border:green_border) +
                ';padding:7px 10px;font-weight: bold;color:' +
                (point.isHighSpeed?yellow_text:green_text)
            "
          >
            {{ point.projectName }}
          </div>
        </div>
      </div>
      <div
        v-show="linePoints.length && linePoint.markerIsShown"
        v-for="linePoint in linePoints"
        :key="linePoint.id"
        :style="
          'width: 17px; height: 40px; position: absolute; z-index: 1; background: url(' +
            yollow_point +
            ');' +
            linePoint.style
        "
        :id="linePoint.id"
      >
        <div
          v-if="linePoint.toolotipIsShown"
          :style="
            'width:' +
              (linePoint.projectName.length * 13 + 55) +
              'px;padding:0px 0px 0px 18px;text-align:center;cursor:pointer;'
          "
          @click="goToTuPu(linePoint.id)"
        >
          <div
            :style="
              'border: 1px solid ' +
                yellow_border +
                ';padding:7px 10px;font-weight: bold;color:' +
                yellow_text
            "
          >
            {{ linePoint.projectName }}
          </div>
        </div>
      </div>
    </div>
    <!-- 图例 -->
    <div class="tl-style">
      <img src="../../assets/center/map/green_point2.png" class="img-style">
      <span class="text-style">项目点</span>
      <br>
      <img src="../../assets/center/map/yollow_point2.png" class="img-style">
      <span class="text-style">线路项目点</span>
      <br>
      <div class="line-style"></div>
      <span class="text-style">项目线路</span>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      yollow_point: require("../../assets/center/map/yollow_point2.png"),
      green_point: require("../../assets/center/map/green_point2.png"),
      green_border: "#47CD8A",
      green_text: "#46CE8A",
      yellow_border: "#FDE25C",
      yellow_text: "#FCB33A",
      map: null,
      view: null,
      pointFromArc: null,
      //项目点的数据，points存放点的样式和id，pointFeatures为点的features
      points: [],
      // pointFeatures: null,
      //项目线的数据，linePoints存放点的样式和id，lineFeatures为线的features
      linePoints: [],
      dx: 9,
      dy: 650,
      // lineFeatures: null
    };
  },
  mounted() {
    this.initMap();
  },
  methods: {
    async initMap() {
      const lineUrl =
        "http://10.10.208.6:9000/Api/map?type=zgxmline&str=&xmlx=";
      const pointUrl =
        "http://10.10.208.6:9000/Api/map?type=zgxmpoint&&str=&xmlx=";

      const esriLoader = await import("esri-loader");

      const arcUnits = await esriLoader.loadModules(
        [
          "esri/Map",
          "esri/views/MapView",
          "esri/Basemap",
          "esri/layers/VectorTileLayer",
          "esri/layers/GeoJSONLayer",
          "esri/geometry/Point",
        ],
        {
          url: "https://zrzyhghj3.jiaxing.gov.cn/arcgis/api/4.12/dojo/dojo.js",
        }
      );

      let Map = arcUnits[0];

      let MapView = arcUnits[1];

      let Basemap = arcUnits[2];

      let VectorTileLayer = arcUnits[3];

      let GeoJSONLayer = arcUnits[4];

      let Point = arcUnits[5];

      this.pointFromArc = Point;

      //蓝色底图
      const blueBase = new VectorTileLayer({
        url:
          "http://10.22.230.26//arcgis/rest/services/Hosted/LANTILE/VectorTileServer",
      });
      //蓝色注解
      const blueZJ = new VectorTileLayer({
        url:
          "http://10.22.230.26//arcgis/rest/services/Hosted/LANZJTILE/VectorTileServer",
      });

      let basemap = new Basemap({
        baseLayers: [blueBase, blueZJ],
      });
      this.map = new Map({ basemap: basemap, layers: [] });

      this.view = new MapView({
        // center: [120.75118324144519, 30.748809193792756],
        map: this.map,
        container: "center-map1",
        zoom: 12,
        constraints: {
          minZoom: 10,
        },
      });
      //等view加载完成，否则取不到spatialReference坐标系
      this.view.when(async () => {
        // Updates the view's center point to a pre-determined Point object
        const pt = new Point({
          x: 120.76218324144519,
          y: 30.768808193792755,
          spatialReference: this.view.spatialReference,
        });
        this.view.center = pt;
        //加载线图层
        this.add_GeoJsonLayer(lineUrl, GeoJSONLayer);
        //  this.add_GeoJsonLayer(pointUrl, GeoJSONLayer);
        //请求得到点数据
        const pointFeatures = await this.getFeatures(pointUrl);
        //请求得到线数据
        // const lineFeatures = await this.getFeatures(lineUrl);
        //存放点数据
        // this.pointFeatures = pointFeatures.features;
        //存放线数据
        // this.lineFeatures = lineFeatures.features;
        //渲染点
        this.renderPointOnMap(pointFeatures.features);
        //渲染线
        // this.renderLinePointOnMap(lineFeatures.features);
        //开启循环
        this.startInterval([this.CarouselForPoint]);
        //监听地图，重新渲染点位置
        this.watchDiv();
      });
      //去除esri copyright
      this.view.ui.remove("attribution");
      //去除地图缩放
      this.view.ui.remove("zoom");
      //   }
      // );
    },
    add_GeoJsonLayer(url, GeoJSONLayer) {
      const layer = new GeoJSONLayer({
        url: url,
        spatialReference: this.view.spatialReference,
      });
      this.map.layers.add(layer);
    },
    getFeatures(url) {
      try {
        return new Promise((resolve, reject) => {
          this.http.get(url).then((res) => {
            if (res.status === 200) {
              resolve(res.data);
            } else {
              reject(res);
            }
          });
        });
      } catch (err) {
        // return (e.message)
        alert("服务器出错");
        console.log(err);
      }
    },
    renderPointOnMap(features) {
      if (features && features.length) {
        let Point = this.pointFromArc;
        for (let i = 0; i < features.length; i++) {
          let mapPoint = new Point({
            x: features[i].geometry.coordinates[0], //后台的经纬度
            y: features[i].geometry.coordinates[1], //后台的经纬度
            spatialReference: this.view.spatialReference,
          });
          let screenPoint = this.view.toScreen(mapPoint);
          if (screenPoint == null) continue;
          const dx = screenPoint.x - this.dx;
          const dy = screenPoint.y - this.dy;
          let Mytransform = null;
          Mytransform = `transform:translate3d(${dx}px,${dy}px, 0);`;
          this.points.push({
            style: Mytransform,
            id: features[i].properties.prjguid,
            projectName: features[i].properties.xmmc,
            toolotipIsShown: i == 0 ? true : false,
            x: features[i].geometry.coordinates[0],
            y: features[i].geometry.coordinates[1],
            markerIsShown: true,
            isHighSpeed: features[i].properties.xmmc.startsWith("嘉兴市市区快速路环线工程")
          });
        }
      } else {
        return false;
      }
    },
    renderLinePointOnMap(features) {
      if (features && features.length) {
        let Point = this.pointFromArc;
        for (let i = 0; i < features.length; i++) {
          let geometry =
            features[i].geometry.coordinates[0][
              parseInt(features[i].geometry.coordinates[0].length / 2)
            ];
          let mapPoint = new Point({
            x: geometry[0], //后台的经纬度
            y: geometry[1], //后台的经纬度
            spatialReference: this.view.spatialReference,
          });
          let screenPoint = this.view.toScreen(mapPoint);
          if (screenPoint == null) continue;
          const dx = screenPoint.x - this.dx;
          const dy = screenPoint.y - this.dy;
          let Mytransform = null;
          Mytransform = `transform:translate3d(${dx}px,${dy}px, 0);`;
          this.linePoints.push({
            style: Mytransform,
            id: features[i].properties.prjguid,
            projectName: features[i].properties.xmmc,
            toolotipIsShown: i == 0 ? true : false,
            x: geometry[0],
            y: geometry[1],
            markerIsShown: true,
          });
        }
      }
    },
    changeTransform(arr, evt) {
      let Point = this.pointFromArc;
      if (arr && arr.length) {
        for (let item of arr) {
          let mapPoint = new Point({
            x: item.x, //后台的经纬度
            y: item.y, //后台的经纬度
            spatialReference: this.view.spatialReference,
          });
          //得到点的位置
          let screenPoint = this.view.toScreen(mapPoint);
          if (screenPoint == null) continue;
          const dx = screenPoint.x - this.dx;
          const dy = screenPoint.y - this.dy;
          let Mytransform = null;
          Mytransform = `transform:translate3d(${dx}px,${dy}px, 0);`;
          item.style = Mytransform;
          //计算点是不是在地图范围内
          item.markerIsShown = evt.contains(mapPoint);
        }
      }
    },
    watchDiv() {
      this.view.watch("extent", (evt) => {
        //调整点的位置
        this.changeTransform(this.points.concat(this.linePoints), evt);
      });
    },
    startInterval([...funs]) {
      setInterval(() => {
        funs.forEach(fun=>{
          fun();
        })
      }, 10000);
    },
    CarouselForPoint() {
      if (this.points && this.points.length) {
        for (let i = 0; i < this.points.length; i++) {
          if (this.points[i].toolotipIsShown) {
            this.points[i].toolotipIsShown = false;
            if (i == this.points.length - 1) {
              this.points[0].toolotipIsShown = true;
            } else {
              this.points[i + 1].toolotipIsShown = true;
            }
            break;
          }
        }
      }
    },
    CarouselForLine() {
      if (this.linePoints && this.linePoints.length) {
        for (let i = 0; i < this.linePoints.length; i++) {
          if (this.linePoints[i].toolotipIsShown) {
            this.linePoints[i].toolotipIsShown = false;
            if (i == this.linePoints.length - 1) {
              this.linePoints[0].toolotipIsShown = true;
            } else {
              this.linePoints[i + 1].toolotipIsShown = true;
            }
            break;
          }
        }
      }
    },
    goToTuPu(projectId) {
      console.log(projectId);
      window.open(`http://10.10.208.6:7090/Home/Index?prjid=${projectId}`)
    },
  },
};
</script>

<style lang="scss" scoped>
#center-map1 {
  // background-image: url("../../assets/center/map/bg_map.png");
  width: 100%;
  height: 96%;
  background-repeat: no-repeat;
  .tl-style{
    background: rgba(0,38,74,0.40);
    box-shadow: inset 0 0 12px 0 rgba(4,160,254,0.40);
    border-radius: 4px;
    width: 8.69rem;
    height: 12.38rem;
    position: absolute;
    left: 61rem;
    top: 35rem;
  }
  .img-style{
    margin-left: 1rem;
  }
  .text-style{
    margin-left: 1rem;
    font-family: PingFangSC-Regular;
    font-size: 12px;
    color: #BED7FA;
    letter-spacing: 0;
    line-height: 40px;
  }
  .line-style{
    width: 0.21rem;
    height: 1.77rem;
    border: 1.5px solid #FDE25C;
    border-radius: 4px;
    float: left;
    margin: 1rem 0.5rem 0rem 1.55rem;
  }
}
</style>

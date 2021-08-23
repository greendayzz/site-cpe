<template>
  <div id="map">
    <div class="equipments">
      <el-card class="box-card"></el-card>
      <el-card class="box-card"></el-card>
    </div>
    <div class="theme">
      <el-radio-group v-model="theme" @change="map_theme" size="small">
        <el-radio-button label="light-v10"
          ><i class="el-icon-sunset"></i
        ></el-radio-button>
        <el-radio-button label="dark-v10"
          ><i class="el-icon-moon-night"></i
        ></el-radio-button>
      </el-radio-group>
    </div>
    <div id="container" ref="basicMapbox"></div>
  </div>
</template>
<script>
import mapboxgl from "mapbox-gl";
export default {
  name: "AppMap",
  data() {
    return {
      map: null,
      theme: "light-v10",
    };
  },
  mounted() {
    this.map_config();
    this.map_marker();
  },
  methods: {
    /*
     *@description: Mapbox Init
     *@author: Lelliam
     *@date: 2021-08-22 23:42:47
     *@param none
     *@version V1.0.5
     */
    map_config() {
      mapboxgl.accessToken =
        "pk.eyJ1IjoicWFzaW01NyIsImEiOiJjanZzMTN4YmYwbTJoNDRtc3lveTUycjR5In0.NHo5uv7_XQpM7fPEus_M-w";
      this.map = new mapboxgl.Map({
        container: this.$refs.basicMapbox,
        // style: 'light-v10',// 'light-v10','dark-v10','outdoors-v11','satellite-v9'
        style: "mapbox://styles/mapbox/light-v10", //地图样式自定义
        center: [100.732971, 38.465042], // 地图中心自定义
        zoom: 4, // 设置地图比例
        //pitch:50
      });
    },

    /*
     *@description: Change Theme
     *@author: Lelliam
     *@date: 2021-08-23 00:10:13
     *@param
     *@version V1.0.5
     */
    map_theme(name) {
      this.map.setStyle(`mapbox://styles/mapbox/${name}`);
      // console.log(name);
    },

    /*
     *@description: Add Marker
     *@author: Lelliam
     *@date: 2021-08-23 00:47:00
     *@param
     *@version V1.0.5
     */
    map_marker() {
      let marker1 = new mapboxgl.Marker({
        draggable: false,
        color: "#0080ff",
      })
        .setLngLat([100.732971, 38.465042])
        .addTo(this.map);

      let marker2 = new mapboxgl.Marker({
        draggable: false,
        color: "#ff3333",
      })
        .setLngLat([99.732971, 34.465042])
        .addTo(this.map);

      marker1._element.setAttribute(
        "class",
        "mapboxgl-marker mapboxgl-marker-anchor-center" + " markID1"
      );
      marker2._element.setAttribute(
        "class",
        "mapboxgl-marker mapboxgl-marker-anchor-center" + " markID2"
      );

      Array.from(marker1._element.querySelectorAll('svg g g[transform="translate(8.0, 8.0)"] circle')).forEach(el=>el.setAttribute('r','8'))
   
      let text = document.createElementNS('http://www.w3.org/2000/svg', 'text');
      text.innerHTML = '3';
      text.setAttribute('x','0.15em')
      text.setAttribute('y','0.8em')
      marker1._element.querySelector('svg g g[transform="translate(8.0, 8.0)"]').appendChild(text)
            

      // this.map_update_marker()
     

    },

    /*
     *@description: Update Marker
     *@author: Lelliam
     *@date: 2021-08-23 00:47:14
     *@param
     *@version V1.0.5
     */
    map_update_marker() {
      // Array.from(this.$el.querySelectorAll('.markID1')).forEach(d=>d.style.display = 'none')
      Array.from(this.$el.querySelectorAll('.markID1')).forEach(d=>d.style.display = 'none')

    },
  },
};
</script>
<style scope>
@import url("../../node_modules/mapbox-gl/dist/mapbox-gl.css");
#map {
  width: 100%;
  height: 100%;
}
#container {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
  height: 100%;
}

.equipments {
  position: absolute;
  width: 80%;
  height: 10%;
  z-index: 1;
  margin: auto;
}

.box-card {
  float: left;
  margin: 10px;
  width: 40%;
  height: 100%;
}

.theme {
  position: absolute;
  right: 0;
  z-index: 1;
}
</style>

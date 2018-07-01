<template>
  <div class="map" id="container">
    
  </div>
</template>

<script>
import bikeLogo from '../assets/bike.png'
export default {
  name: 'hello',
  data () {
    return {
      
    }
  },
  methods: {
    addMarker: function(map, point){  // 创建图标对象   
      var myIcon = new BMap.Icon(bikeLogo, new BMap.Size(46, 50), {  
         anchor: new BMap.Size(10, 25),    
       });      
      // 创建标注对象并添加到地图   
       var marker = new BMap.Marker(point, {icon: myIcon});    
       map.addOverlay(marker);    
    }  
  },
  mounted() {
    var map = new BMap.Map("container");          // 创建地图实例  
    var point = new BMap.Point(116.404, 39.915);  // 创建点坐标  

    // 定位
    var self = this;
    var geolocation = new BMap.Geolocation();
    geolocation.getCurrentPosition(function(r){
      if(this.getStatus() == BMAP_STATUS_SUCCESS){
        // alert('您的位置：'+r.point.lng+','+r.point.lat);
        point = new BMap.Point(r.point.lng, r.point.lat);
      }
      else {
        alert('failed'+this.getStatus());
      }  
      // 初始化地图，设置中心点坐标和地图级别        
      map.centerAndZoom(point, 15);        

      self.addMarker(map, point);
    },{enableHighAccuracy: true})
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
#container {
  height: 100%;
}
.BMap_Marker div {
  border-radius: 50%;
}
.BMap_Marker img {
  width: 100%;
}
</style>

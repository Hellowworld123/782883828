<template>
  <div class="detail">
    <h2>车辆编号：{{$route.params.id}}</h2>
    <h2>故障信息：{{$route.params.detail}}</h2>
    <mt-checklist
      title=""
      v-model="method"
      :options="['更换二维码', '更换轮胎', '更换其他配件']">
    </mt-checklist>
    <mt-button type="primary" @click="repairDone" size="large">维修完成</mt-button>
    <mt-button type="default" @click="back" size="large">返回</mt-button>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
    	method: []
    }
  },
  methods: {
  	repairDone() {
  		let id = this.$route.params.id;
  		let method = this.method;
  		fetch(`/api/repair?id=${id}&method=${method}`)
  		.then((res)=>{
  			return res.json();
  		}).then((json)=>{
  			console.log(json);
  			if(json.message) {
  				alert(json.message);
  			}
  		})
  	},
  	back() {
  		this.$router.push({path: "/"});
  	}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.mint-button--large {
  width: 90%;
  margin: 10px auto 0 auto;
}
.mint-checklist {
  text-align: left;
}
.detail h2 {
  text-align: left;
  padding-left: 5%;
}
.detail {
  background: url(../assets/home_bg2.jpg) no-repeat -200px center;
}
</style>

<template>
  <div class="map-contain" ref="mapContain"></div>
</template>

<script>
	import { defineComponent, onMounted, ref } from 'vue';
	import * as echarts from 'echarts';
	import mapData from '../assets/map/world-china.json';

	export default defineComponent({
		name: 'IndexDemo',
		components: {},
		setup() {

			const mapContain = ref(null);

			// 争议线
			/* const JDaStyle = {
				name: "ZY", 
				itemStyle: {
					normal: {
						opacity: 1, // 透明度
						borderColor: "#040812", // 省份界线颜色
						borderWidth: 4, // 省份界线的宽度
						borderType: 'dashed',
						areaColor: 'rgba(0,0,0,0)', // 整个省份的颜色
					},
				},
			} */
			

			// 中国地图样式
			const chinaStyle = {
				name: "China", 
				itemStyle: {
					normal: {
						opacity: 1, // 透明度
						borderColor: "#5b5c63", // 中国界线颜色
						borderWidth: 4, // 中国界线的宽度
						areaColor: 'rgba(0,0,0,0)', // 整个中国的颜色
					},
				},
			}

			// 省份
			const provinceArr = ['河北','山西','辽宁','吉林','黑龙江','江苏','浙江','安徽','福建','江西','山东','河南','湖北','湖南','广东','海南','四川','贵州','云南','陕西','甘肃','青海','台湾','内蒙古','广西','西藏','宁夏','新疆','北京','天津','上海','重庆','香港','澳门'];

			let regionsJson = [];
			regionsJson = provinceArr.map(( item ) => {
				return {
						name: item, 
						label: {
							show: true,
							formatter: function(params){
								return params.name;
							},
							color: '#4d4c4c',
							fontSize: 11,
							align: 'center',
							verticalAlign: 'middle'
						},
						itemStyle: {
							borderColor: '#283158',
							borderWidth: 1,
						}
					}
			})
			regionsJson.push(chinaStyle);
			// regionsJson.push(JDaStyle);

			const canvasGeo = () => {
				echarts.registerMap('world', mapData);
				let chart = echarts.init(mapContain.value);
				let option = {
					backgroundColor: '#09152a',
					title: {
						text: '',
						left: 'center',
						textStyle: {
							color: '#fff'
						}
					},
					geo: {
						map: 'world',
						roam: true,
						zoom: 4.8,
						center: [106.086897, 36.451049],
						label: {
							emphasis: {
								show: false
							}
						},
						silent: true, // 图形是否不响应和触发鼠标事件 false：响应和触发鼠标事件
						regions: regionsJson, // 在地图中对特定的区域配置样式
						itemStyle: {
							normal: {
								areaColor: '#040812',
								borderColor: '#4d4c4c',
							},
							emphasis: {
								areaColor: '#2a333d'
							}
						}
					},
				};
				chart.setOption(option);
			};

			onMounted(async () => {
				await canvasGeo();
			})

			return { mapContain }
		}
	})
</script>

<style>
	.map-contain {
		width: 100%;
		height: 100%;
	}
</style>

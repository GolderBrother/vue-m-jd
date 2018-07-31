<template>
	<div id="cate_left">
		 <div class="category_left">
	            <ul class="childbox">
	                <li :class="{childboxli:item.flag}" :key="i" v-for="(item,i) in leftDatas" @click="categoryClass(item,i)">
	                	<router-link :to="'/catgory/'+item.category_id">
	                	{{item.category_name}}
	                	</router-link>
	                </li>
	               
	            </ul>
	        </div>
	</div>
</template>
<script>
export default{
	data() {
		return{
			leftDatas:[],
			childboxli:'childboxli'
		}
	},
	//生命周期
	mounted() {
		this.getLeftDatas();
	},
	methods:{
		async getLeftDatas() {
			try {
				const _this = this;
				const result = await _this.$http.get('/category');
				if(result.data && result.data.length){
					this.leftDatas = result.data;
					this.leftDatas.forEach((item,index) => {
						_this.$set(item,'flag',false)
					})
				}
			} catch (error) {
				console.log(error)
			}
			// this.$http.get('/category').then((res)=>{
			// 	//console.log(res);
			// 	this.leftDatas = res.data;
			// 	for(let i=0;i<this.leftDatas.length;i++){
			// 		//this.leftDatas[i].flag=false;
			// 		this.$set(this.leftDatas[i],'flag',false);
			// 	}
			// },(err)=>{
			// 	console.log(err);
			// })
		},
		categoryClass(item,index){
			//$().addClass().siblings().removeClass();
			const _this = this;
			_this.leftDatas.forEach((leftDatas,i) => {
				_this.$set(leftDatas,'flag',false);
				if(index == i){
					item.flag = true;
				}
			})
			// for(let i=0;i<this.leftDatas.length;i++){
			// 	this.$set(this.leftDatas[i],'flag',false);
			// 	if(index == i){
			// 		item.flag = true;
			// 	}
			// }
		}

	}
}
</script>
<style>
	#cate_left .category_left .childbox .childboxli{
		background:#f60;
	}
</style>
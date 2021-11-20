<template>
	<div>
		<div class="addItem">
			<input type="text" v-model="item.name" />
			<font-awesome-icon 
				icon="plus-square"
				@click="addItem()"
				:class="[item.name? 'active' : 'inactive', 'plus']"
			/>
		</div>
	</div>
</template>
<script>
	export default{
		data: function(){
			return {
				item: {
					name:""
				}
			}
		},
		methods:{
			addItem(){
				// console.log(this.item.name);
				if(this.item.name === ''){
					return;
				}
				axios.post('api/items/store', {
					item: this.item
				})
				.then(response => {
					if(response.status == 201){
						this.item.name = "";
						this.$emit('reloadlist');
					}
				})
				.catch(error => {
					console.log(error);
				})
			}
		}
	}
</script>
<style type="text/css">
	.addItem{
		display: flex;
		justify-content: center;
		align-items: center;
	}
	input{
		background: #f7f7f7;
		border: 0;
		outline: none;
		padding: 5px;
		margin-right: 10px;
		width: 100%;
	}
	.plus{
		font-size: 20px;
	}
	.active{
		color: #00CE25;
	}
	.inactive{
		color: #9999;
	}
</style>
<template>
	<view style="width:100%;">
		<picker mode="selector" @change="_pickerChange" :value="atindex" :range="picklist.Name" class="uni-rows">
			{{picklist.Name[atindex]}}
		<!-- 	{{accordValue}} -->
		</picker>
	</view>
</template>

<script>
	var _self;
	export default {
		data() {
			return {
				picklist:{},
				atindex:0,
				actualValue: '0',
				accordValue: '0',
			};
		},
		name: 'uni-picker',
		props: {
			list: {
				type: Object,
				default:function(){
						return{
							itemName: '示例1',
							itemId: 12,
							
						}
				}
			},
			index: {
				type: [Number,String],
				default: 0
			}
		},
		created() {
			_self=this;
			_self.picklist=_self.list;
			_self.atindex=_self.index;
			_self.actualValue = _self.picklist.Id[Number(_self.index)];
			_self.accordValue = _self.picklist.Name[Number(_self.index)];
		},
		watch:{
			list: function(list,index) {
				_self.picklist = _self.list;
				_self.atindex=_self.index;
			}
		},
		methods: {
			_pickerChange(e) {
				const i = Number(e.detail.value);
				_self.atindex = i;
				_self.actualValue = _self.picklist.Id[i];
				_self.accordValue = _self.picklist.Name[i];
				_self.emit(_self.actualValue, _self.accordValue);
			},
			emit(actualValue, accordValue) {
				_self.$emit('change', {
					actualValue: actualValue,
					accordValue: accordValue
				});
			}
		}
	}
</script>

<style>
	.uni-rows {
		width: 100%;
	}
</style>

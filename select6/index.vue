
<template>
	<Select
        filterable
        remote
        :remote-method="FEHPVBremoteMethod"
    >
        <Option v-for="item in FEHPVBcityList" :value="item.value" :key="index">{{item.label}}</Option>
    </Select>
</template>
<script>
export default { 
	data(){
		return {
			FEHPVBcityList: [
                {
                    value: 'NewYork',
                    label: 'NewYork'
                },
                {
                    value: 'London',
                    label: 'London'
                }
            ]
		}
	},
    methods:{
        FEHPVBremoteMethod(v){
            
        }
    }
}
</script>

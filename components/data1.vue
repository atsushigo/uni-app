<template>
	<t-table border="2" border-color="#95b99e" :is-check="true" @change="change">
		<t-tr font-size="14" color="#95b99e" align="left">
			<t-th align="left">姓名</t-th>
			<t-th align="left">年龄</t-th>
			<t-th align="left">爱好</t-th>
			<t-th align="center">操作</t-th>
		</t-tr>
		<t-tr font-size="12" color="#5d6f61" align="right" v-for="item in tableList" :key="item.id">
			<t-td align="left">{{ item.name }}</t-td>
			<t-td align="left">{{ item.age }}</t-td>
			<t-td align="left">{{ item.hobby }}</t-td>
			<t-td align="left"><button @click="edit(item)">编辑</button></t-td>
		</t-tr>
	</t-table>
</template>

<script>
	import tTable from '@/components/t-table/t-table.vue';
		import tTh from '@/components/t-table/t-th.vue';
		import tTr from '@/components/t-table/t-tr.vue';
		import tTd from '@/components/t-table/t-td.vue';
		
		export default {
			components:{
				data1
			}
		}
</script>

<style>
</style>

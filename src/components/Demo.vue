<template>
	<list items="dataArray" width="300" height="300" rowHeight="20" rowRender=""></list>
</template>

<script>
import list from './List'

export default {
	data() {
		return {
			dataArray: new Array(1000).fill('This is a long ass string')
		};
	},
	methods: {
		rowRender: function(index, offset) {
			return '<div style="position:absolute; top:{{ offset }}">{{ this.dataArray[index] }}</div>'
		}
	}
}
</script>
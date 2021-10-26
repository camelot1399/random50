<template>
  <div>
		<table>
			<thead>
				<tr>
					<td>Наименование</td>
					<td>Цена</td>
					<td>Количество</td>
					<td>Стоимость</td>
				</tr>
			</thead>
			<tbody>
				<tr v-for="item of data" :key="item.id">
					<td>{{ item.name }}</td>
					<td>{{ item.price }}</td>
					<td>{{ item.count }}</td>
					<td>{{ (item.price * item.count).toFixed(2) }}</td>
				</tr>
			</tbody>
		</table>

		<div>Итоговая стоимость: <span>{{ totalPrice }}</span></div>
  </div>
</template>

<script>
export default {
	name: 'tableComponent',
	props: {
		data: {
			type: Array
		}
	},
	computed: {
		totalPrice() {
			return this.data.reduce((acc, item) => {
				return acc + (item.price * item.count);
			}, 0).toFixed(2)
		}
	},
	mounted() {
		console.log(this.data);
	}
}
</script>

<style>
table {
    border: 1px solid #ccc;
}
td {
    color: black;
    border-right: 1px dashed #ccc;
    padding: 10px 20px;
}
tbody > tr {
    border-bottom: 1px solid #ccc;
}
</style>
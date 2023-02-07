<script setup>
	import Card from './Card.vue';
	import axios from 'axios';
	import { ref, watch, onMounted } from 'vue';

	const BASE_URL = 'https://api.got.show'
	const characters = ref(null);
	const charactersOnPage = ref(null);
	const page = ref(1);

	const imageNotFound = 'https://upload.wikimedia.org/wikipedia/commons/thumb/6/65/No-Image-Placeholder.svg/480px-No-Image-Placeholder.svg.png';

	const characterPerPage = 12;

	const outerVisible = ref(false)
	const innerVisible = ref(false)

	const currentCharacter = ref(null)

	onMounted(async () => {
		const response = await axios.get(`${BASE_URL}/api/book/characters`);
		characters.value = response.data;

		const start = (page.value - 1) * characterPerPage;
		const end = start + characterPerPage;
		charactersOnPage.value = characters.value.slice(start, end);
	});

	watch(page, () => {
		const start = (page.value - 1) * characterPerPage;
		const end = start + characterPerPage;
		charactersOnPage.value = characters.value.slice(start, end);
	});


</script>


<template>
	<div class="container">
		  <div v-loading="!charactersOnPage" class="cards">
			  <Card
				  v-for="character in charactersOnPage"
				  :key="character._id"
				  :image="character.image ? character.image : imageNotFound"
				  :name="character.name"
				  :onClick="() => {
					  currentCharacter = character
					  outerVisible = true
				  }"
			  />
  
		  </div>
		  <div class="button-container">
			  <button @click="page--">&lt;</button>
			  <button @click="page++">></button>
		  </div>
	  </div>

	  <el-dialog v-model="outerVisible" :title="currentCharacter?.name">
		<template #default>
			<el-dialog
				v-model="innerVisible"
				width="30%"
				title="Inner Dialog"
			/>

			<div class="d-content">
				<div class="d-img">
					<img :src="currentCharacter?.image ? currentCharacter?.image : imageNotFound" alt="" />
				</div>
				<div class="d-info">
					<div v-if="currentCharacter?.house">
						<h3>House</h3>
						<p>{{ currentCharacter?.house }}</p>
					</div>

					<div v-if="currentCharacter?.books.length">
						<h3>Books</h3>
						<p v-for="book in currentCharacter?.books" :key="book">{{ book }}</p>
					</div>
				</div>
			</div>
		</template>
	</el-dialog>
</template>


<style scoped>

	.d-content {
		display: flex;
		align-items: center;
	}

	.d-img {
		width: 50%;
	}

	.d-img img {
		width: 100%;
	}

	.d-info {
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;

		width: 50%;

		padding: 20px;
	}

	.d-info div {
		display: flex;
		flex-direction: column;
		align-items: center;

		padding: 15px;
	}

	.d-info div h3 {
		font-size: 20px;
		font-weight: bolder;
	}

	.d-info div p {
		font-size: 10px;
		text-align: center;
	}
	.container {
		background-color: rgb(27, 26, 26);
		padding: 30px;
		min-height: 100vh;
	}
	.cards {
		max-width: 1000px;
		margin: 0 auto;
		display: flex;
		flex-wrap: wrap;
		justify-content: center;
	}
	.cards h3 {
		font-weight: bold;
	}
	.cards p {
		font-size: 10px;
	}
	.button-container {
		display: flex;
		justify-content: center;
		padding-top: 30px
	}
	.button-container button {
		border: none;
		width: 50px;
		height: 50px;
		border-radius: 100%;
		margin: 0 5px;
		cursor: pointer;
	}
</style>
<script setup>
	import { defineProps, defineEmits } from 'vue';

	const emit = defineEmits(['selectPlatform'])


	const { isShow } = defineProps([
		'isShow'
	])

	const emitSelectedPlatform = () => {
		emit('selectPlatform')
	}

</script>


<template>
	<div class="hero">
		<h1>Game of Thrones</h1>
		<p @click="emitSelectedPlatform">{{ isShow ? 'Tv Show' : 'Book' }} Characters</p>
	</div>
</template>


<style scoped>
	.hero {
    height : 40vh;
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    flex-direction: column
	}
	.hero h1 {
		font-size: 100px;
		font-weight: bold;
	}
	.hero p {
		cursor: pointer;
	}
</style>
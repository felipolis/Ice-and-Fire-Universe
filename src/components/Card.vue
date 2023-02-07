<script setup>
    import { defineProps } from 'vue';

    const { image, name } = defineProps([
        'image',
        'name'
    ])
</script>


<template>
    <div>
        <el-card :body-style="{ padding: '0px' }">
            <div>
                <img :src="image" class="image"/>
            </div>
            <div style="padding: 14px;">
                <span class="name">{{ name }}</span>
            </div>
        </el-card>
    </div>
</template>


<style scoped>

    * {
        box-sizing: border-box;
        padding: 0;
        margin: 0;
    }
    .el-card {
        width: 200px;
        height: 380px;
        margin:10px 20px;
        cursor: pointer;
    }
    
    .image {
        /* cover */
        width: 100%;
        height: 300px;
        object-fit: cover;
        display: block;
    }

    .name {
        display: block;
        text-align: center;
    }

    /* Se passar o mouse sobre o card, aumente ele */
    .el-card:hover {
        transform: scale(1.05);
        transition: all 0.3s ease-in-out;
    }

</style>
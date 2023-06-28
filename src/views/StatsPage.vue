<script>
import axios from 'axios';
import dayjs from 'dayjs';

export default {
    data() {
        return {
            categories: []
        }
    },
    mounted() {
        this.loadCateries()
    },
    methods: {
        async loadCateries() {
            let response = await axios.get('/stats');
            this.categories = response.data;
            console.log(this.categories)
        }
    }
}
</script>


<template>
    <div class="create-page">
        <h3 class="mb-5">Сводка</h3>
            <div class="categories-container my-5">
                <label v-for="(item, index) in categories" class="category">
                    <input class="category-input" name="category" type="radio" :value="item._id">
                    <div class="category-info">
                        <h1>{{ item.stats }}</h1>
                        <img class="mt-5" :src="'src/assets/' + item.value + '.svg'">
                        {{ item.title }}
                    </div>
                </label>
            </div>
    </div>
</template>


<style>
.create-page h3 {
    text-align: center;
}

.create-page .category {
    display: flex;
    flex-direction: column;
    width: 20%;
    align-items: center;
    justify-content: center;
}

.category {
    position: relative;
}

.category img {
    width: 60%;
}

.category-input {
    display: none;
}


.category-info {
    display: flex;
    flex-direction: column;
    gap: 10px;
    align-items: center;
    justify-content: center;
    padding: 10px;

    transition: scale 300ms;
}

/* Выбранная радиокнопка */
.category .category-input:checked~.category-info {
    scale: 1.4;
}

.categories-container {
    display: flex;
}

.note-container {
    display: flex;
    gap: 10px;
    justify-content: space-between;
}

.note-container .note-input-container {
    flex: 1;
}
</style>
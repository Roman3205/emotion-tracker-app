<script>
import axios from 'axios';
import dayjs from 'dayjs';

export default {
    data() {
        return {
            notes: []
        }
    },

    mounted() {
        this.loadNotes()
    },

    methods: {
        async loadNotes() {
            let response = await axios.get('/notes/all')
            this.notes = response.data
        },

        getRelativeDate(date) {
            let day = dayjs(date).format('YYYY-MM-DD hh:mm')
            return day
        }
    }
}
</script>

<template>
    <div class="calendar-page">
        <div class="card my-3">
            <div class="card-body" v-for="(item) in notes" >
                <img :src="'src/assets/' + item.category.value + '.svg'">
                <div>
                    <div class="note-title">
                        {{ item.category.title }}
                    </div>
                    <div class="note-date">
                        {{ getRelativeDate(item.date) }}
                    </div>
                    <p class="note-text">
                        {{ item.text }}
                    </p>
                </div>
            </div>

        </div>
    </div>
</template>


<style>
.calendar-page .card-body {
    display: flex;
    gap: 40px;
    align-items: flex-start;
}

.calendar-page img {
    width: 100px;
}

.calendar-page .note-title {
    font-weight: bold;
    text-transform: uppercase;
    font-size: 24px;
    ;
}

.calendar-page .note-date {
    text-transform: lowercase;
    color: #6c757d;
}

.calendar-page .note-text {
    margin-top: 10px;
}
</style>
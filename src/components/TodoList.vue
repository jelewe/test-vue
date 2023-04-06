<script setup>
    defineProps({
        task: String,
        note: String,
        importance: String,
        date: new Date(),
        done: Boolean,
        id: Number
    })

    defineEmits(['toggleDone', 'remove'])

</script>

<template>
    <div class="card" :class="{ completed: done }" :id="[id]" >
        <div class="priority" :class="[importance]"></div>
            <div class="top">
                <input type="checkbox" :id="[id]" @change="$emit('toggleDone', id)" />
                <div class="taskItem"> 
                    {{ task }} 
                </div>
                <button type="button" @click="$emit('remove', id)">X</button>
            </div>
            <div class="subs"> 
                {{ note }} {{ date }} 
            </div>
    </div>
</template>

<style scoped>

    .card {
        border-radius: 3px;
        border: 1px solid rgba(84, 84, 84, 0.48);
        display: grid;
        grid-template-columns: 1rem 1fr;
        grid-template-rows: 1fr 1fr;
        margin-bottom: 0.5rem;
        padding-right: 0.4rem;
    }

    .completed {
        text-decoration: line-through;
    }

    .top {
        display: flex;
        margin-left: 0.2rem;
        grid-area: 1 / 2 / 2 / 3;
    }

    .taskItem {
        padding-left: 0.2rem;
    }

    .subs {
        padding-left: 1.2rem;
        grid-area: 2 / 2 / 3 / 3;
    }

    .priority {
        grid-area: 1 / 1 / 3 / 2;
    }

    .High {
        background: #ce2525;
    }

    .Medium {
        background: #ff6600;
    }

    .Low {
        background: #f1c550;
    }




</style>
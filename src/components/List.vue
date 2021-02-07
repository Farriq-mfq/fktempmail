<template>
    <div>
        <div class="daftar__email" v-for="list in lists" :key="list.id">
            <b-icon icon="egg-fill" class="icon__mail"></b-icon>
            <router-link :to="`view/${list.id}`" @click="msg()" class="list_email">
                <span>{{list.subject}}</span>
                <span>{{list.from}}</span>
                <span>{{list.date}}</span>
            </router-link>
            <b-icon icon="arrow-right" ></b-icon>
        </div>
    </div>
</template>

<script>
export default {
    name:'List',
    props:['lists'],
    
}
</script>

<style>

</style>
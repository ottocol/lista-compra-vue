<template>
    <ul>
        <li v-for="i in items" :key="i.id">
            <item :id="i.id" :nombre="i.nombre"/>
        </li>
    </ul>
</template>


<script>
import Item from './Item.vue'

export default {
    name: 'Lista',
    components: {
        Item
    },
    props: ['items']
}
</script>


<style scoped>

</style>
<template>
    <div class="app">
        <z-row>
            <h1>this is row</h1>
        </z-row>
    </div>
</template>

<script>
export default {
    name:'app',
    components: {
        zRow:()=>import('./components/layout/row/src/row.vue')
    }
}
</script>

<style scoped>

</style>
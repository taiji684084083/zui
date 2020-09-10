<template>
    <div class="app">
        <z-row>
           <z-col></z-col>
        </z-row>
    </div>
</template>

<script>
export default {
    name:'app',
    components: {
        zRow:()=>import('./components/layout/row/row.vue'),
        zCol:()=>import('./components/layout/col/col.vue')
    }
}
</script>

<style scoped>

</style>
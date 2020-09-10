<template>
    <div class="app">
        <z-row>
           <z-col :span="12" :xs="{span:6,pull:6}" class="hidden-xs-only"></z-col>
           <z-col :style="{background:'green'}" :span="12" :xs="{span:6,pull:6}" class="hidden-xs-only"></z-col>
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
.z-col{
    background: green;
}
.z-col{
    height: 300px;
    background: red;
}
</style>
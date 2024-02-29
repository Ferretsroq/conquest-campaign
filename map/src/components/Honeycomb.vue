<script setup>
    import Hexagon from './Hexagon.vue';
 
    



    const hexWidth = 50;
    const hexHeightCornerpx = `${Math.floor(-(hexWidth/2)*1/Math.sqrt(3))}px`;
    const hexWidthHalfpx = `${Math.floor(hexWidth/2)}px`;
    defineOptions({
  inheritAttrs: false
});
    const rows = 10;
    const numHexes = 20;
    const rowIndexList = [];
    const hexIndexList = [];

    for(let index = 0; index < rows; index++)
    {
        rowIndexList.push(index);
    }
    for(let index = 0; index < numHexes; index++)
    {
        hexIndexList.push(index);
    }
   
</script>

<template>
    <div class="rows">
        <!--<div class="row" v-for="i in 5">
            <Hexagon v-for="j in 5" :hexWidth="hexWidth" />
        </div>-->
        <div class="row" v-for="row in rowIndexList">
            <Hexagon v-for="hex in hexIndexList" :hexWidth="hexWidth" :hexID="(row*numHexes)+hex" />
        </div>
    </div>
</template>
<style>
.row {
    margin-bottom: v-bind(hexHeightCornerpx);
    display: flex;
}
.row:nth-child(odd) {
    margin-left: v-bind(hexWidthHalfpx);
}
</style>
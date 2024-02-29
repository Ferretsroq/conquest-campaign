<script setup lang="ts">
import {ref, computed} from 'vue';


const clicks = ref(0);
const props = defineProps({
  hexWidth: Number,
  hexID: Number
});
const hexWidth = props.hexWidth;
const hexID = props.hexID;
const hexHeight = hexWidth*Math.sqrt(3)/2*2/3;

const hexWidthpx = `${hexWidth}px`;
const hexHeightpx = `${hexWidth*Math.sqrt(3)/2*2/3}px`;
const hexMarginpx = `${hexWidth*Math.sqrt(3)/2*1/3}px 0`;
const hexAfterpx = `${hexWidth*Math.sqrt(2)/2}px`;
const hexAfterLeftpx = `${(hexWidth/2) - ((hexWidth/2)*Math.sqrt(2)/2)}px`;
const hexToppx = `${-(hexWidth/2)*Math.sqrt(2)/2}px`;

const factions = ['Spires', 'City States'];

let owner = factions[Math.floor(Math.random()*factions.length)];

const color = ChooseColor(owner);

function ChooseColor(owner)
{
  if(owner == 'Spires')
  {
    return 'rgba(255, 186, 74, 0.1)';
  }
  else if(owner == 'City States')
  {
    return 'rgba(0, 128, 51, 0.1)';
  }
}


function nodeClick(nodeId: any)
{
  console.log(nodeId);
  clicks.value++;
}



</script>
<template>

<div >
  <div class="hexagon" @click.stop="$parent.$emit('hexClick', owner)">
    <!--<div class="label">
      {{ hexID }}
    </div> -->
    <!--<div class="graph" :id="`hexID${hexID}`">
      <Graph :value="diagram" @node-click="nodeClick" :hexWidthpx="hexWidthpx" :hexHeightpx="hexHeightpx"/>
    </div>-->
  </div>
</div>
</template>

<style>
.label {
  font-size: 24px;
  text-align: center;
  position: relative;
  z-index: 2;
  color: #cccccc;
}
.hexagon {
  position: relative;
  width: v-bind('hexWidthpx'); 
  height: v-bind('hexHeightpx');
  background-color: v-bind('color');
  margin: v-bind('hexMarginpx');
  border-left: solid 1px #ffffff;
  border-right: solid 1px #ffffff;
}

.hexagon:before,
.hexagon:after {
  content: "";
  position: absolute;
  z-index: 1;
  width: v-bind('hexAfterpx');
  height: v-bind('hexAfterpx');
  -webkit-transform: scaleY(0.5774) rotate(-45deg);
  -ms-transform: scaleY(0.5774) rotate(-45deg);
  transform: scaleY(0.5774) rotate(-45deg);
  background-color: inherit;
  left: v-bind(hexAfterLeftpx);
}

.hexagon:before {
  top: v-bind(hexToppx);
  border-top: solid 1px #ffffff;
  border-right: solid 1px #ffffff;
}

.hexagon:after {
  bottom: v-bind(hexToppx);
  border-bottom: solid 1px #ffffff;
  border-left: solid 1px #ffffff;
}
</style>
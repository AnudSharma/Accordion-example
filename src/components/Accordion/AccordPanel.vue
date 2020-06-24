<template>
<div>
    <!-- <h1>Accord Example</h1> -->
  <div class="accord-panel">
      <template>
        <div @click="toggle(!visible)">
    <accord-head  class="accord-head" >
              <slot name="header" />
      </accord-head>
        </div>
        <transition-expand>
 <accord-section class="accord-section" v-if="visible">
           <slot />
      </accord-section>
        </transition-expand>
       
    </template>
  </div>
</div>

</template>

<script>
import AccordHead from "../Accordion/AccordHead";
import AccordSection from "../Accordion/AccordSection";
import TransitionExpand from "../Accordion/TransitionExpand";
export default {
  components: {
    AccordHead,
    AccordSection,
    TransitionExpand,
  },
data(){
    return {
        visible:false,
       
    }
},

beforeMount(){ //when a new component is mounted, we register the panel object with wrapper
    this.$parent.register(this);
},
beforeDestroy(){
    this.$parent.unregister(this)
},
methods:{
    toggle(value){ //value=true
        // console.log("toggling")
        // this.visible=!this.visible
        if(value!=this.visible)//conditions falls true
        {
this.visible=value;
this.$parent.setOpen(this,this.visible);
        } 
    },
}

 
};
</script>
<style scoped>
    .accord-panel {
        box-shadow: 1px 1px 2px #aaa;
        background: white;
        margin-bottom: 3px;
    }

     .accord-panel +  .accord-panel {
        margin-top: 0.5em;
    }

    .accord-head{
        padding: 0.5em;
        background-color: rgb(71, 145, 206);
    }

    .accord-section {
        border-top: 1px solid #ccc;
        background-color: lightgray;
    }

     .accord-head {
        cursor: pointer;
    }
</style>
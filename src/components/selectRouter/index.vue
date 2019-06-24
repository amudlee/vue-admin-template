
<template>
<div class="selectRouter ">
  <div style="padding: 0 15px;" @click="toggleClick">
    <svg v-if="isOpen" class="icong" aria-hidden="true">
        <use xlink:href="#icon-food-pudding"></use>
    </svg>
    <svg v-else="!isOpen" class="icong" aria-hidden="true">
        <use xlink:href="#icon-food-doughnut"></use>
    </svg>
  </div>
 
</div>
</template>

<script>
export default {
  name: 'Hamburger',
  data(){
      return {
          isOpen:false
      }
  },
  methods:{
      toggleClick(){
          this.isOpen = !this.isOpen
          this.$emit('toggleMenu',this.isOpen)
      }
  }
}
</script>

<style scoped>
.selectRouter {
    position: relative;
}

.icong {
    width: 20px; height: 20px;
    fill: currentColor;
    overflow: hidden;
    vertical-align: middle;
    }


</style>

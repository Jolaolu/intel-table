<template>
  <div id="view-more-container"  :class="[hover ? 'show' : 'hide' ]">
    <div class="view-more">View Project</div>
  </div>
</template>

<script>
export default {
  name: "ViewMore",
  props:['hover']
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#view-more-container {
  filter: blur(0);
  width: 10rem;
  position: relative;
  right: 35rem;
  margin-top: 1rem
  
}
.show{
  display: flex;
}
.hide{
 display: none;
}

.view-more {
  width: 100%;
  border: 1px solid #2a3a49;
  display: flex;
  justify-content: center;
  padding: 0.8rem 0.5rem;
}
</style>

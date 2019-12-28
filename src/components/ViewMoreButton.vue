<template>
  <div id="view-more-container" :class="[hover ? 'show' : 'hide' ]">
    <div class="view-more">View Project</div>
  </div>
</template>

<script>
export default {
  name: "ViewMore",
  props: ["hover"]
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
 #view-more-container {
  filter: blur(0);
  margin-top: 1rem;
  cursor: pointer;
  font-weight: 700;
}
@media (max-width: 767px) {
  #view-more-container {
    width: auto;
    position: absolute;
    right: .2rem;
  }
}
@media (min-width: 768px) and (max-width: 1024px) {
  #view-more-container {
    width: auto;
    position: absolute;
    right: 17rem;
  }
}
@media (min-width: 1025px) {
  #view-more-container {
  filter: blur(0);
  width: auto;
  position: absolute;
  right: 35rem;
  margin-top: 1rem;
  cursor: pointer;
  font-weight: 700;
}
}

.show {
  display: flex;
}
.hide {
  display: none;
}

.view-more {
  width: 10rem;
  border: 1px solid #2a3a49;
  color: #2a3a49;
  border-radius: 0.3rem;
  display: flex;
  justify-content: center;
  padding: 0.5rem 0.5rem;
}
</style>

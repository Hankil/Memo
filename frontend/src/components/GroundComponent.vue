<template>
  <div class="ground">
    <HeaderComponent />
    <MemoComponent />
    <FooterComponent />
  </div>
</template>

<script>
import HeaderComponent from './HeaderComponent.vue';
import FooterComponent from './FooterComponent.vue';
import MemoComponent from './MemoComponent.vue';
export default {
  components: { HeaderComponent, FooterComponent, MemoComponent },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

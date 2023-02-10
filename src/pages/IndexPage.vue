<template>
  <transition
    appear
    enter-active-class="animated zoomIn"
    leave-active-class="animated zoomOut"
  >
    <q-page class="flex column flex-center">
      <img
        alt="Quasar logo"
        src="~assets/faced.png"
        style="width: 300px; height: 160px"
      />
      <h4 class="">Sistema de Geração de Termo de Empréstimo</h4>
    </q-page>
  </transition>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "IndexPage",
});
</script>

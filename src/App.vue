<template>
  <router-view />
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "App",
});
</script>
<style>
@media print {
  body * {
    visibility: hidden;
  }
  .principal,
  .principal * {
    visibility: visible;
  }
  .principal {
    position: fixed;
    left: 0;
    top: 0;
    margin-top: 80px;
    margin-left: 60px;
  }
}
</style>
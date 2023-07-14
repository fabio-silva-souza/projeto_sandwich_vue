<template>
<banner />
  <div class="main-container">
    <h1>Monte seu Lanche !</h1>
    <lanches-form />
   </div>
</template>

<script>
import Banner from '@/components/Banner.vue'
import LanchesForm from '@/components/LanchesForm.vue'
export default {
  name: 'Home',
  components: {
    Banner,
    LanchesForm
  }
}
</script>

    LanchesForm
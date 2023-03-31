<template>
<banner />
  <div class="main-container">
    <h1>Monte seu Sandwich ich</h1>
    <sandwich-form />
   </div>
</template>

<script>
import Banner from '@/components/Banner.vue'
import SandwichForm from '@/components/SandwichForm.vue'
export default {
  name: 'Home',
  components: {
    Banner,
    SandwichForm
  }
}
</script>

    SandwichForm
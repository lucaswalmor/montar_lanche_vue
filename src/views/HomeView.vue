<template>
  <div class="main-container">
    <Banner></Banner>
    <h1>Monte o seu lanche:</h1>
    <BurguerForm></BurguerForm>
    
  </div>
</template>

<script>
import Banner from '@/components/Banner.vue';
import BurguerForm from '../components/BurguerForm.vue';
export default {
    components: { Banner, BurguerForm }
}
</script>

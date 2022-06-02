<template>
  <div class="mainBanner">
      <h1>Make Your Burguer</h1>
  </div>
</template>

<script>
export default {
name: "Banner",
}
</script>

<style scoped>
.mainBanner{
    background-image: url('/img/burger.jpg');
    background-position: 0% 60%;
    background-size: cover;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    height: 500px;
}

.mainBanner h1{
    color: white;
    font-size: 60px;
    text-align: center;
    background-color: #222;
    padding: 20px 40px;
    
}

</style>
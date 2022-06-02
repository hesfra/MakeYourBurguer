<template>
  <footer id="footer">
      <p>Make Your Burguer &copy; 2022</p>
  </footer>
</template>

<script>
export default {
name: "Footer",
}
</script>

<style scoped>
#footer{
  position: sticky;
  height: 60px;
  background-color: #222;
  border-top: 4px solid #111;
  color:#fcba03;
  display: flex;
  justify-content: center;
  align-items: center;
  bottom:0;
  width:100%;
  margin-top:50px;
}

</style>
<template>
  <div>
    <div class="container">
      <div class="row" :key="i" v-for="(item,i) in images">
        <img :src="item.largeImageURL"><br>
         <strong>Tags: </strong><span> {{item.tags}} </span><br>
         <strong>Like: </strong><span> {{item.likes}} </span><br>
         <strong>User: </strong><span> {{item.user}} </span>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["images"]
};
</script>

<style scoped>
img{
  padding-top: 20px;
  width: 600px;
  height: 400px;
}
</style>

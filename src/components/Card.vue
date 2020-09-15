<template>
  <div class="card">
      <header class="card-header">
          <p class="card-header-title">{{name}}</p>
      </header>
      <div class="card-content">
          <div class="content">{{description}}</div>
      </div>
  </div>
</template>

<script>
export default {
    name: 'Card',
    props: ['name', 'description'],
    data: function(){
        return {
            n:null
        }
    }
}
</script>

<style>

</style>
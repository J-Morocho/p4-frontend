<template>
  <div class="card">
      <header class="card-header">
          <p class="card-header-title">{{name}}</p>
      </header>
      <div class="card-content">
          <div class="content">{{description}}</div>
      </div>
      <v-card-actions>
      <v-btn text>Button</v-btn>
      </v-card-actions>
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
.card-header-title {
    font-size: 10px;
}
</style>
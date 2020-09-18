<template>
  <div class="card">
      <p class="card-header-title">{{name}}</p>
      <div class="card-content">
          <div class="content">{{description}}</div>
      </div>
      <footer class="card-footer">
          <a class="card-footer-item up">Water Plant</a>
          <a class="card-footer-item up">Edit</a>
          <a class="card-footer-item del">Delete</a>
      </footer>
      
  </div>
</template>

<script>
export default {
    name: 'Card',
    props: ['name', 'description'],
    data: function(){
        return {
            category_id: null,
        }
    }
}
</script>

<style>
.card-header-title {
    font-size: 10px;
}

.del {
    color: red;
}

.up {
    color: #26537e;
}

</style>
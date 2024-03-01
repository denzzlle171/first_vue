<script>
export default {
  name: 'MyButton'
}
</script>

<template>
  <button class="btm">
    <slot></slot>
  </button>
</template>

<style scoped>
.btm {

  align-items: center;
  padding: 10px 15px;
  background: none;
  color: teal;
  border: 1px solid teal;
}

</style>
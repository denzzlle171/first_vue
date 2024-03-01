<script>
// import MyButton from '@/components/UI/MyButton.vue'

export default {
  // components: {
  //   MyButton
  // },
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
};
</script>

<template>
  <div class="post">
    <div>
      <div>{{ post.id }}</div>
      <div><strong>{{ post.title }}</strong></div>
      <div>{{ post.body }}</div>
    </div>
    <div class="post__btn">
      <MyButton @click="$emit('remove', post )">delete</MyButton>
    </div>
  </div>
</template>

<style>
.post {
  border: 3px solid green;
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 8px;
}


</style>

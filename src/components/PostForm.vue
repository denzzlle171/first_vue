<script>
// import MyButton from '@/components/UI/MyButton.vue'

export default { 
  // components: {
  //   MyButton
  // },
  data() {
    return {
      post: {
        title: '',
        body: '',
      }
      
    }
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit('create', this.post)
      this.post = {
      title : '',
      body : '',
      }
    
    }
  }
}
</script>

<template>
  <form @submit.prevent>
  <h3>create post</h3>
  <MyInput 
    v-model="post.title"
    type="text"
    placeholder="name post"
  />
  <MyInput 
    v-model="post.body"
    type="text" 
    placeholder="describe" 
  />
  <MyButton @click="createPost">create</MyButton>
</form>
</template>

<style>

</style>
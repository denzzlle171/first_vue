<script>
import PostItem from '@/components/PostItem.vue';
export default {
  components: { PostItem },
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
};
</script>

<template>
  <div v-if="posts.length > 0">
    <h3>list of users</h3>
    <TransitionGroup name="post-user">
      <PostItem
        class="post"
        v-for="post in posts"
        :post="post"
        :key="post.id"
        @remove="$emit('remove', post)"
      />
    </TransitionGroup>
  </div>
  <h2 class="danger" v-else>the posts list is empty</h2>
</template>

<style>
.danger {
  color: red;
}

/* .post-user-enter-active,
.post-user-leave-active {
  transition: all 0.5s ease;
}
.post-user-enter-from,
.post-user-leave-to {
  opacity: 0;
  transform: translateX(30px);
} */
.post-user-move, /* застосувати перехід до рухомих елементів */
.post-user-enter-active,
.post-user-leave-active {
  transition: all 0.5s ease;
}

.post-user-enter-from,
.post-user-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

/* переконайтеся, що кінцеві елементи вилучено з потоку, щоб перемістити
  анімації можна правильно розрахувати. */
/* .post-user-leave-active {
  position: absolute;
} */

</style>

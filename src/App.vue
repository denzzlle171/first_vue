<script>
import PostForm from '@/components/PostForm.vue';
import PostList from '@/components/PostList.vue';
import MyButton from './components/UI/MyButton.vue';
import MySelect from './components/UI/MySelect.vue';
import axios from 'axios';

export default {
  components: {
    PostForm,
    PostList,
    MyButton,
    MySelect,
  },
  data() {
    return {
      posts: [],
      modalVisible: false,
      isPostLoading: false,
      selectedSort: '',
      searchQuery: '',
      page: 1,
      limit: 10,
      totalPages: 0,
      sortOptions: [
        { value: 'title', name: 'Name' },
        { value: 'body', name: 'Content' },
      ],
    };
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.modalVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter((p) => p.id !== post.id);
    },
    showDialog() {
      this.modalVisible = true;
    },
    chagePage(pageNumber) {
      this.page = pageNumber
    },

    async fetchPosts() {
      try {
        this.isPostLoading = true;
        setTimeout(async () => {
          const response = await axios.get(
            'https://jsonplaceholder.typicode.com/posts',
            {
              params: {
                _page: this.page,
                _limit: this.limit,
              },
            }
          );
          this.totalPages = Math.ceil(
            response.headers['x-total-count'] / this.limit
          );
          this.posts = response.data;
          this.isPostLoading = false; //
        }, 1000);
      } catch (e) {
        alert('warn !!!!!');
      } finally {
        // this.isPostLoading = false
      }
    },
  },
  mounted() {
    this.fetchPosts();
  },

  computed: {
    sortedPosts() {
      return [...this.posts].sort((a, b) => {
        return a[this.selectedSort]?.localeCompare(b[this.selectedSort]);
      });
    },
    sortedAndsearchedPost() {
      return this.sortedPosts.filter((post) =>
        post.title.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },

  watch: {
    page() {
      this.fetchPosts()
    }
  },
};
</script>

<template>
  <div>
    <h2>posts page</h2>
    <MyInput v-model="searchQuery" placeholder="search..." />
    <div class="app__buttons">
      <MyButton @click="showDialog"> create post </MyButton>
      <MySelect v-model="selectedSort" :options="sortOptions"></MySelect>
    </div>

    <MyDialog v-model:show="modalVisible">
      <PostForm @create="createPost" />
    </MyDialog>

    <PostList
      :posts="sortedAndsearchedPost"
      @remove="removePost"
      v-if="!isPostLoading"
    />
    <p v-else>...Dowloding...</p>
    <div class="page__wraper">
      <div
        v-for="pageNumber in totalPages"
        :key="pageNumber"
        class="page"
        :class="{
          'current-page': page === pageNumber,
        }"
        @click="chagePage(pageNumber)"
      >
        {{ pageNumber }}
      </div>
    </div>
  </div>
</template>

<style>
.app__buttons {
  display: flex;
  justify-content: space-between;
}
.page__wraper {
  display: flex;
  margin-top: 15px;
}
.page {
  border: 1px solid teal;
  padding: 10px;
}
.current-page {
  background-color: #ed92b0;
}
</style>

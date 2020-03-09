<template>
  <div id="stories">
      <Story v-for="(storyId, index) in storyIds" :key="storyId"
        :story-id="storyId"
        :showIt="showIt(index)"
        v-on:is-shown="isShown(storyId)"
      />
  </div>
</template>

<script>
import Story from './Story.vue';

export default {
  name: 'Stories',
  components: {
    Story
  },
  props: {
  },
  data: function () {
      return {
        storyIds: [],
        shownIds: [],
      }
  },
  methods: {
    getStories() {
      fetch('https://hacker-news.firebaseio.com/v0/newstories.json')
          .then((response) => {
              return response.json();
          })
          .then((myJson) => {
              this.storyIds = myJson;
          });
    },
    showIt(index) {
      return index == 0 || this.shownIds.includes(this.storyIds[index - 1]);
    },
    isShown(id) {
      this.shownIds.push(id);
    }
  },
  created: function () {
    this.getStories();
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>

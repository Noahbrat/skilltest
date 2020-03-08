<template>
  <div id="stories">

  </div>
</template>

<script>
export default {
  name: 'Stories',
  props: {
  },
  data: function () {
      return {
        storyIds: []
      }
  },
  methods: {
    getStories: function () {
      fetch('https://hacker-news.firebaseio.com/v0/newstories.json')
          .then((response) => {
              return response.json();
          })
          .then((myJson) => {
              this.storyIds = myJson;
          });
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

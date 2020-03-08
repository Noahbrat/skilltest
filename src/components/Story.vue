<template>
  <div class="story">
      {{storyId}}
  </div>
</template>

<script>
export default {
  name: 'Story',
  props: ['storyId'],
  data: function () {
      return {
        story: {},
      }
  },
  methods: {
    getStory() {
      fetch(`https://hacker-news.firebaseio.com/v0/item/${this.storyId}.json`)
          .then((response) => {
              return response.json();
          })
          .then((myJson) => {
              this.story = myJson;
          });
      }
  },
  created: function () {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>

<template>
  <div v-on:click.stop="getStory()">
      <div v-if="story.id" class="story">
          <a :href="story.url" target="_blank">{{story.title}}</a>
            <span class="author"> by {{story.by}}</span>
            <span class="time"> at {{new Date(story.time * 1000) | dateFormat('h:mma')}}</span>
      </div>
      <div v-else-if="this.showIt" class="story-loader" v-observe-visibility="visibilityChanged">
          {{storyId}}
      </div>
  </div>
</template>

<script>
import Vue from 'vue';
import VueFilterDateFormat from 'vue-filter-date-format';
import VueObserveVisibility from 'vue-observe-visibility'
Vue.use(VueFilterDateFormat);
Vue.use(VueObserveVisibility);

export default {
  name: 'Story',
  props: ['storyId', 'showIt'],
  data: function () {
      return {
        story: {},
      }
  },
  methods: {
    visibilityChanged(isVisible) {
        if (isVisible) {
            this.getStory();
        }
    },
    getStory() {
      fetch(`https://hacker-news.firebaseio.com/v0/item/${this.storyId}.json`)
          .then((response) => {
              return response.json();
          })
          .then((myJson) => {
              this.story = myJson;
              this.$emit('is-shown')
          });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.story {
    padding: .25em .5em;
    margin: .5em;
    background-color: #eee;
    border: solid 1px #ddd;
    border-radius: .25em;
}

.author {
    font-style: italic;
    color: navy;
    white-space: nowrap;
}
.time {
    color: navy;
    white-space: nowrap;
}

a {
    font-size: 1.5em;
    color: green;
    text-decoration: none;
}

.story-loader {
    font-size: 2em;
    padding: .5em;
    margin: .5em;
    color: white;
}

</style>

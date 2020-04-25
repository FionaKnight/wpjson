<template>
  <div class="post">
    <h2>{{wppost.title.rendered}} ({{wppost.acf.year}})</h2>
    <img
      :src="wppost._embedded['wp:featuredmedia'][0].media_details.sizes.full.source_url"
      :alt="wppost.title.rendered"
    />
    <p>{{wppost.acf.description}}</p>
    <div v-for="(item, index) in wppost._embedded['wp:term']" :key="index">
      <div v-if="index < 3">
        <h3>{{item[0].taxonomy.charAt(0).toUpperCase() + item[0].taxonomy.slice(1) + ((item.length > 1) ? "s" : "")}}</h3>
        <ul>
          <li v-for="subitem in item" :key="subitem.id">{{subitem.name}}</li>
        </ul>
      </div>
      <div v-else>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "PostItem",
  props: ["wppost"],
  data() {
    return {
      myGenre: []
    };
  }
};
</script>

<style lang="scss" scoped>
.post {
  margin: 0.8em 0.2em;
  padding: 1em;
  box-sizing: border-box;
  box-shadow: 0 19px 38px rgba(0, 0, 0, 0.3), 0 15px 12px rgba(0, 0, 0, 0.22);
  background-color: rgba(255, 224, 179, 0.2);
}

h2,
p {
  width: 90%;
  padding: 0;
  margin: 5px auto;
}

div {
  text-align: left;
}

img {
  width: 100%;
  padding: 0;
  max-width: 90px;
  height: auto;
  margin: 0 auto;
  display: block;
}

@media only screen and (min-width: 450px) {
  .post {
    width: calc(50% - 0.8em);
  }
}

@media only screen and (min-width: 900px) {
  .post {
    width: calc(33% - 1em);
  }
}
</style>
<template>
  <div id="pokemon">

    <div class="card">
      <div class="card-image">
        <figure>
          <img
            :src="pokemon.front"
            alt="Placeholder image"
          />
        </figure>
      </div>
      <div class="card-content">
        <div class="media">
          <div class="media-left">
            <span>{{ num }}</span>
          </div>
          <div class="media-content">
            <p class="title is-4">{{ upper(name) }}</p>
            <p class="subtitle is-6">{{ pokemon.type }}</p>
          </div>
        </div>

        <div class="content">
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  created: function () {
    axios
      .get(this.url)
      .then((res) => {
        this.pokemon.type = res.data.types[0]?.type.name;
        this.pokemon.front = res.data.sprites.front_default;
        this.pokemon.back = res.data.sprites.back_default;
      })
      .catch((err) => {
        console.log(err);
      });
  },
  data() {
    return {
      pokemon: {type:'', front:'', back:''},
    };
  },
  props: {
    num: Number,
    name: String,
    url: String,
  },
  methods: {
    upper: function (value) {
      return value[0].toUpperCase() + value.slice(1);
    },
  },
};
</script>

<style scoped>
    #pokemon {
        margin-bottom: 10px;
    }
</style>
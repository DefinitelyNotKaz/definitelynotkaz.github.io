<template>
  <div id="card">
    <b-card :title="name" :img-src="image" img-alt="Image" img-top tag="article" class="mb-2 fixed">
      <b-card-text>
        Some quick example text to build on the card title and make up the bulk of the card's content.
      </b-card-text>

      <b-button v-if="active" href="#" variant="primary">Open</b-button>
      <div v-else  id="archive-buttons">
        <b-button :href="image" variant="primary">Full size</b-button>
        <b-button v-if="timelapse !== ''" :href="timelapse" variant="primary">Timelapse</b-button>
      </div>
    </b-card>
  </div>
</template>

<script>
export default {
  name: "Card-New",
  props: {
    image: {
      type: String,
      required: true
    },
    name: {
      type: String,
      required: true
    },
    active : {
      type: Boolean,
      required: true
    },
    template: {
      type: String,
      required: false
    },
    timelapse: {
      type: String,
      required: false
    }
  }
}
</script>

<style scoped>
.fixed {
  max-width: 19rem;
}

.fixed > img {
  width: 100%;
  height: auto;
  max-height: 10rem;
  object-fit: contain;
  image-rendering: pixelated;
}

#archive-buttons {
  display: flex;
  justify-content: center;
  gap: 1em;
}
</style>
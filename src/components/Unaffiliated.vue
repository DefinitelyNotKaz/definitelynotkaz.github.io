<template>
  <b-media>
    <template #aside>
      <b-img id="logos" :src="image"></b-img>
      <div id="content">
        <h5 id="name" class="mt-0">{{ title }}</h5>
        <div id="urls">
          <b-button size="sm" variant="info" :href="url">
            Open
          </b-button>
        </div>
      </div>
    </template>
  </b-media>
</template>

<script>


export default {
  name: "Unaffiliated-Templates",
  props: {
    title: {
      type: String,
      require: true
    },
    url: {
      type: String,
      require: true,
    },
    image: {
      props: String,
      require: true
    },
  },
  methods: {
    templateExists(template) {
      return template && template.length > 0;
    },
    templateNotExists(template) {
      return !this.templateExists(template)
    }
  }
}
</script>

<style scoped>
#display {
  display: flex;
  flex-direction: column;
}

#name {
  margin-bottom: 0;
}

#content {
  margin-left: 1em;
}

#logos {
  width: 3.5rem;
  height: auto;
  border-radius: 10px;
  image-rendering: pixelated;
}

#urls {
  display: flex;
  gap: .5em;
}

#ally-template {
  width: 5em;
}
</style>
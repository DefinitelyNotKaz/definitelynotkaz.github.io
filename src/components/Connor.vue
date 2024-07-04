<template>
  <div id="content" class="container">
    <b-alert v-if="inactive" show variant="danger"><b-icon-exclamation-triangle-fill></b-icon-exclamation-triangle-fill>
      This event has ended! The page now is a public archive!</b-alert>
    <h1>Timelapse</h1>
    <hr>
    <div id="timelapse-container">
      <video controls on-pause="true" src="/connor/timelapses/full.mp4"></video>
    </div>
    <h1>Templates</h1>
    <hr>
    <div id="card-container">
      <Card v-for="(item, index) in displayedTemplates" :key="index" :image="item.image" :name="item.name"
        :timelapse="item.timelapse" :active="item.active"></Card>
      <b-button class="card-section-btn" variant="primary" v-if="showSeeMoreTemplatesButton"
        @click="showMoreTemplates">See more</b-button>
      <b-button class="card-section-btn" variant="primary" v-if="showSeeLessTemplatesButton"
        @click="showLessTemplates">See less</b-button>
    </div>
    <hr>
    <b-container>
      <b-row>
        <b-col>
          <h1>Unnoficial</h1>
          <hr>
          <div id="ally-container">
            <Unaffiliated v-for="(item, index) in displayedUnaffiliated" :key="index" :title="item.name"
              :image="item.image"></Unaffiliated>
          </div>
          <b-button class="card-section-btn" style="margin-top: 1em;" variant="primary"
            v-if="showSeeMoreUnaffiliatedButton" @click="showMoreUnaffiliated">See more</b-button>
          <b-button class="card-section-btn" style="margin-top: 1em;" variant="primary"
            v-if="showSeeLessUnaffiliatedButton" @click="showLessUnaffiliated">See less</b-button>
        </b-col>
        <b-col>
          <h1>Allies</h1>
          <hr>
          <div id="ally-container">
            <Ally v-for="(item, index) in displayedAllies" :key="index" :title="item.name" :details="item.url"
              :image="item.image" :templates="item.preview"></Ally>
          </div>
          <b-button class="card-section-btn" style="margin-top: 1em;" variant="primary" v-if="showSeeMoreAlliesButton"
            @click="showMoreAllies">See more</b-button>
          <b-button class="card-section-btn" style="margin-top: 1em;" variant="primary" v-if="showSeeLessAlliesButton"
            @click="showLessAllies">See less</b-button>
        </b-col>
      </b-row>
    </b-container>
    <hr>
    <h1>Abandoned Templates</h1>
    <hr>
    <div id="card-container">
      <Card v-for="(item, index) in displayedDeprecated" :key="index" :image="item.image" :name="item.name"
        :active="item.active" :timelapse="item.timelapse"></Card>
      <b-button class="card-section-btn" variant="primary" v-if="showSeeMoreDeprecatedButton"
        @click="showMoreDeprecated">See more</b-button>
      <b-button class="card-section-btn" variant="primary" v-if="showSeeLessDeprecatedButton"
        @click="showLessDeprecated">See less</b-button>
    </div>
  </div>
</template>

<script>
import { BIconExclamationTriangleFill } from 'bootstrap-vue'

import Card from './Items.vue'
import Ally from './Allies.vue'
import Unaffiliated from './Unaffiliated.vue'

export default {
  name: "Connor-Canvas",
  components: {
    BIconExclamationTriangleFill,
    Card,
    Ally,
    Unaffiliated
  },
  data() {
    return {
      inactive: true,
      showMoreTemplatesButton: true,
      templates: [
        { image: '/connor/templates/chainsaw.png', timelapse: '/connor/timelapses/Chainsaw_Neuro.mp4', name: "Chainsaw Neuro", active: false },
        { image: '/connor/templates/evilIDF.png', timelapse: '/connor/timelapses/Evil_IDF.mp4', name: "Evil IDF", active: false },
        { image: '/connor/templates/sleepover.png', timelapse: '/connor/timelapses/Miyu_Sleep.mp4', name: "Moon Sleepover", active: false },
        { image: '/connor/templates/channy.png', timelapse: '/connor/timelapses/Channy_Fumo.mp4', name: "Channy & Fumo", active: false },
        { image: '/connor/templates/annyhood.png', timelapse: '', name: "Anny Hoodie", active: false },
        { image: '/connor/templates/gigavedal.png', timelapse: '/connor/timelapses/Gigavedal_Anny.mp4', name: "Giga Vedal & Anny", active: false },
        { image: '/connor/templates/swarm.png', timelapse: '', name: "Swarm Calls", active: false },
        { image: '/connor/templates/anny.png', timelapse: '', name: "Anny", active: false },
      ],
      displayTemplateCount: 4,
      allies: [
        { image: '/connor/allies/osu.png', name: "osu!", url: ["https://osu.place/cdawgva"], preview: [] },
        { image: '/connor/allies/vienna.webp', name: "Vienna", url: ["https://tinyurl.com/viennagrimaceshake"], preview: [] },
        { image: '/connor/allies/camila.jpeg', name: "Camila", url: ["https://tinyurl.com/camilARTV3"], preview: ['/connor/allies/templates/camila.png'] },
        { image: '/connor/allies/rainhoe.jpeg', name: "Rainhoe", url: ["https://tinyurl.com/yc3d9jve"], preview: ['/connor/allies/templates/rainhoe.png'] },
        { image: '/connor/allies/false.jpg', name: "FalseEyeD", url: ["https://tinyurl.com/TVStemplate"], preview: [] },
        { image: '/connor/allies/pxls.png', name: "Pxls.Space", url: ["https://tinyurl.com/pxlsspacetemp"], preview: ['/connor/allies/templates/pxls.png'] },
        { image: '/connor/allies/filian.jpg', name: "Filian", url: ["", ""], preview: ['/connor/allies/templates/filian1.png'] },
        {
          image: '/connor/allies/rqmaddie.jpeg', name: "Rqmaddie", url: ["", ""], preview: ['/connor/allies/templates/maddie1.png', '/connor/allies/templates/maddie2.png']
        },
        { image: '/connor/allies/miyune.jpg', name: "Miyune", url: ["", ""], preview: ["", '/connor/allies/templates/miyune2.png'] },
        { image: '/connor/allies/saruei.png', name: "Saruei Corp", url: [""], preview: [] },
      ],
      displayAlliesCount: 5,
      unaffiliated: [
        { image: '/connor/unaffiliated/neuroPls.png', name: "neuroPls", url: "" },
        { image: '/connor/unaffiliated/femturtle.png', name: "Femturtle", url: "" },
        { image: '/connor/unaffiliated/host.png', name: "Host Error", url: "" },
        { image: "/connor/unaffiliated/pipe.png", name: "Emergency Pipe", url: "" },
        { image: '/connor/unaffiliated/studysama.png', name: "Study-sama", url: "" },
        { image: '/connor/unaffiliated/isaac.png', name: "Neuro TBOI", url: "" },
        { image: '/connor/unaffiliated/shiba.png', name: "Shiba", url: "" },
        { image: '/connor/unaffiliated/evilChibi.png', name: "Evil Chibi", url: "" },
        { image: '/connor/unaffiliated/vedalRocket.png', name: "Vedal Rocket", url: "" },
        { image: '/connor/unaffiliated/toff.png', name: "Toff", url: "" },
      ],
      displayUnaffiliatedCount: 5,
      deprecated: [
        { image: '/connor/templates/deprecated/channyEvil.png', name: 'Channy + Evil Fumo', url: '', timelapse: '/connor/timelapses/deprecated/Channy_EvilFumo.mp4', active: false },
        { image: '/connor/templates/deprecated/neuroIDF.png', name: 'Neuro IDF', url: '', timelapse: '/connor/timelapses/deprecated/Neuro_IDF.mp4', active: false },
        { image: '/connor/templates/deprecated/family.png', name: 'Family Table', url: '', timelapse: '/connor/timelapses/deprecated/Family_Table.mp4', active: false },
        { image: '/connor/templates/deprecated/neuro.png', name: 'Neuro', url: '', timelapse: '/connor/timelapses/deprecated/neuro_arts.mp4', active: false },
        { image: '/connor/templates/deprecated/anny.png', name: 'anny', url: '', timelapse: '', active: false }
      ],
      displayDeprecatedCount: 5
    }
  },
  computed: {
    displayedTemplates() {
      return this.templates.slice(0, this.displayTemplateCount)
    },
    showSeeMoreTemplatesButton() {
      return this.displayTemplateCount < this.templates.length;
    },
    showSeeLessTemplatesButton() {
      return this.displayTemplateCount > 4;
    },
    displayedAllies() {
      return this.allies.slice(0, this.displayAlliesCount)
    },
    showSeeMoreAlliesButton() {
      return this.displayAlliesCount < this.allies.length;
    },
    showSeeLessAlliesButton() {
      return this.displayAlliesCount > 5;
    },
    displayedUnaffiliated() {
      return this.unaffiliated.slice(0, this.displayUnaffiliatedCount)
    },
    showSeeMoreUnaffiliatedButton() {
      return this.displayUnaffiliatedCount < this.unaffiliated.length;
    },
    showSeeLessUnaffiliatedButton() {
      return this.displayUnaffiliatedCount > 5;
    },
    displayedDeprecated() {
      return this.deprecated.slice(0, this.displayDeprecatedCount)
    },
    showSeeMoreDeprecatedButton() {
      return this.displayDeprecatedCount < this.deprecated.length;
    },
    showSeeLessDeprecatedButton() {
      return this.displayDeprecatedCount > 5;
    },
  },
  methods: {
    showMoreTemplates() {
      return this.displayTemplateCount += 4;
    },
    showLessTemplates() {
      return this.displayTemplateCount = 4;
    },
    showMoreAllies() {
      return this.displayAlliesCount += 5;
    },
    showLessAllies() {
      return this.displayAlliesCount = 5;
    },
    showMoreUnaffiliated() {
      return this.displayUnaffiliatedCount += 5;
    },
    showLessUnaffiliated() {
      return this.displayUnaffiliatedCount = 5;
    },
    showMoreDeprecated() {
      return this.displayDeprecatedCount += 5;
    },
    showLessDeprecated() {
      return this.displayDeprecatedCount = 5;
    }
  }
};
</script>

<style scoped>
#content {
  margin-bottom: 5em;
}

#timelapse-container {
  display: flex;
  justify-content: center;
}

#timelapse-container>video {
  width: 50%;
}

#card-container {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 1em;
}

#ally-container {
  display: flex;
  flex-direction: column;
  gap: 1em;
}

.card-section-btn {
  max-height: 3em;
}
</style>

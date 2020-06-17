<template>
  <div class="packageCard">
    <v-card
      class="mx-auto text-left"
      @click="selectPackage(singlePackage)"
    >
      <v-card-title>
        <a 
          @click="hrefClickHandler($event)" 
          class="display-1 text--primary" 
          :href="singlePackage.package.links.npm"
          target="_blank"
        >
            {{ singlePackage.package.name }}
        </a>
      </v-card-title>
      <v-card-text>
        <div>{{ singlePackage.package.description }}</div>
      </v-card-text>
      <v-card-actions>
        <v-btn
          text
          color="blue accent-4"
          @click="hrefClickHandler($event)"
          :href="singlePackage.package.links.npm"
          target="_blank"
        >
            Learn More
        </v-btn>
      </v-card-actions>
    </v-card>

    <v-dialog
      v-model="selectedPackage"
      v-if="selectedPackage"
      max-width="560"
    >
      <v-card>
        <v-card-title class="headline">
          <v-row>
            <v-col cols='6'>
              {{ selectedPackage.package.name }}
            </v-col>
            <v-col cols='6'>
              <div class="package-buttons">
                <a 
                  v-for="(item, index) in selectedPackage.package.links" 
                  :key="item + index" 
                  :href="item" 
                  target="_blank" 
                  class="buttons"
                >
                  <v-icon size="24px">{{ `mdi-${linkIcons[index]}` }}</v-icon>
                </a>
              </div>
            </v-col>
          </v-row>

        </v-card-title>

        <v-card-text>
          <div>
            <span class="package-user">
              {{ selectedPackage.package.publisher.username }}
            </span>

            <span class="package-label">
              <img src="https://img.icons8.com/android/16/000000/price-tag.png"/>
              <span>{{ selectedPackage.package.version }}</span>
            </span>
          </div>
        </v-card-text>

        <v-card-text>
          {{ selectedPackage.package.description }}
        </v-card-text>

        <v-card-text v-if="selectedPackage.package.keywords">
          <span v-for="item in selectedPackage.package.keywords" :key="item" class="package-label">
            {{ item }}
          </span>
        </v-card-text>

        <v-card-actions>
          <v-spacer></v-spacer>

          <v-btn
            color="red darken-1"
            text
            @click="selectedPackage = null"
          >
            Close
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: ['singlePackage'],

  name: 'SinglePackage',

  data () {
    return {
      selectedPackage: null,
      linkIcons: {
        bugs: 'bug',
        repository: 'source-repository',
        homepage: 'home',
        npm: 'npm'
      }
    }
  },

  methods: {
    selectPackage(selectedPackage) {
      this.selectedPackage = selectedPackage;
    },

    hrefClickHandler(e) {
      e.stopPropagation();
    }
  }
}
</script>

<style lang="scss">
  .packageCard + .packageCard {
    margin-top: 8px;
  }

  .package-user {
    margin-right: 8px;
  }

  .package-label {
    display: inline-flex;
    border: 1px solid #e5e5e5;
    border-radius: 3px;
    padding: 2px 8px;
    margin-right: 8px;
    margin-bottom: 4px;
    margin-top: 4px;
    max-width: 220px;
    overflow: hidden;
    text-overflow: ellipsis;
    vertical-align: middle;

    span {
      margin-left: 8px;
    }
  }

  .package-buttons {
    float: right;

    .buttons {
      display: inline-flex;
      border: 1px solid #e5e5e5;
      float: left;
      font-size: 20px;
      line-height: 20px;
      text-align: center;
      padding: 10px;
    }

    a {
      text-decoration: none;
    }
  }
</style>

<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">
          Search npm packages
        </h1>

        <v-text-field label="Search all of npm" @keyup="getPackages()" v-model="searchValue"></v-text-field>

        <NoResult 
          v-if="(responseData.length === 0 && responseDataLength === 0 && searchValue) || error" :text="error ? 'Oopz, there was an error!' : 'No results match your query!'"
        />

        <v-card v-for="index in 10" :key="'A' + index">
          <v-skeleton-loader
            v-if="loading && searchValue"
            height="94"
            type="list-item-two-line"
          >
          </v-skeleton-loader>
        </v-card>

        <PackagesList :packages="responseData" :key="componentKey" />

        <v-pagination
          v-model="page"
          v-if="responseDataLength && searchValue"
          class="my-4"
          :length="responseDataLength"
          @input="fetchData()"
        ></v-pagination>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  import axios from 'axios';
  import PackagesList from './PackagesList';
  import NoResult from './NoResult';
  
  export default {
    name: 'MainApp',

    components: {
      PackagesList,
      NoResult
    },

    data: () => ({
      responseData: [],
      responseDataLength: null,
      loading: false,
      searchValue: '',
      _timerId: null,
      componentKey: 0,
      page: 1,
      apiUrl: 'http://registry.npmjs.com/-/v1/search?size=10&text=',
      error: false
    }),
    
    methods: {
      getPackages() {
        this.responseDataLength = null;
        clearTimeout(this._timerId);

        if (!this.searchValue) {
          this.responseData = [];
          return;
        }

        this._timerId = setTimeout(() => {
          this.page = 1;
          this.fetchData();
        }, 500)
      },

      fetchData() {
        const from = (this.page - 1) * 10;
        this.loading = true;
        this.responseData = [];
        window.scrollTo({
          top: 0,
          left: 0,
          behavior: 'smooth'
        });

        axios
          .get(`${this.apiUrl}${this.searchValue}&from=${from}`)
          .then(response => {
            this.responseData = response.data.objects;
            this.responseDataLength = Math.floor(response.data.total / 10);
            this.componentKey += 1;
          })
          .catch(() => this.error = true)
          .finally(() => this.loading = false)
      }
    }
  }
</script>

<style lang="scss">
  .v-card + .v-card {
    margin-top: 8px;
  }
</style>

<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-4">
        <p>{{ text }}</p>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>

export default {
	props: ['text'],

  name: 'NoResult'
}

</script>
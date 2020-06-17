<template>
  <div v-if="packages">
    <SinglePackage v-for="item in packages" :singlePackage="item" :key="item.package.date" />
  </div>
</template>

<script>
  import SinglePackage from './SinglePackage';

  export default {
    props: ['packages'],

    name: 'PackagesList',

    components: {
      SinglePackage,
    },
  }
</script>

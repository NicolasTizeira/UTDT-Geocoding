<template>
<f7-app :params="f7params" >
  <f7-view main class="safe-areas" url="/"></f7-view>

</f7-app>
</template>
<script>

  import routes from '../js/routes.js';

  export default {
    data() {
      return {
        f7params: {
          name: 'GeoCode',
          theme: 'auto',
          routes: routes,
        },
      }
    },
    methods: {
      
    },
    mounted() {
      this.$f7ready((f7) => {
      });
    }
  }
</script>
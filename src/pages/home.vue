<template>
  <f7-page name="home">
    <f7-navbar :sliding="false" large>
      <f7-nav-title sliding>GeoCode</f7-nav-title>
      <f7-nav-title-large sliding>GeoCode</f7-nav-title-large>
    </f7-navbar>
    <br />
    <input
      size="50"
      class="input-address"
      id="Address"
      type="text"
      placeholder="Ciudad de residencia *"
      v-model="address"
    />
    <span v-if="suggestion" v-on:click="selectSuggestion" class="suggestion">{{suggestion}}</span>
    <br />
  </f7-page>
</template>

<script>
var geocoder;
geocoder = new google.maps.Geocoder();

export default {
  data() {
    return {
      address: null,
      suggestion: null
    };
  },
  watch: {
    address: "getSuggestion"
  },
  methods: {
    getSuggestion(value) {
      if (this.suggestion == value) {
        this.suggestion = null;
      } else {
        if (value.length > 2) {
          let self = this;
          geocoder.geocode(
            {
              address: value
            },
            function(results, status) {
              $.map(results, function(item) {
                return (self.suggestion = item.formatted_address);
              });
            }
          );
        }
      }
    },
    selectSuggestion() {
      this.address = this.suggestion;
    }
  }
};
</script>

<style scoped>
.input-address {
  border: 1px solid #ddd;
  height: 2.25em;
  margin-left: 1%;
}

.suggestion {
  margin-left: 1.5%;
  border: #ddd 1px solid;
}
.suggestion:hover {
  background-color: gainsboro;
  cursor: pointer;
}
</style>
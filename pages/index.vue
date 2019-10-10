<template>
  <div class="haederImage">
    <img class="image" src="/images/desert.jpg" />
    <div class="max-w-sm rounded overflow-hidden shadow-lg searchFilterDiv">
      <div class="inline-block relative w-64">
        <select
          v-model="slug"
          class="block appearance-none
           w-full bg-white border border-gray-400
            hover:border-gray-500 px-4 py-2 pr-8 rounded shadow
             leading-tight focus:outline-none focus:shadow-outline">
          <!-- <option selected>choose city</option> -->
          <option v-for="city in citiesInfo"
           :data-slug="city.slug" 
           :key="city.slug"
           :value="city.slug" >
            {{ city.name }}
          </option>
        </select>
      </div>
      <a class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" @click="getSlug"
      >
        Search
      </a>
    </div>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";

export default {
  data() {
    return {
      citiesInfo: null,
      slug:''
    };
  },

  methods: {
    async fetchCities() {
      const url = 'cities'
      const ip = await this.$axios.$get(url)
      .then(res=>{
        this.citiesInfo = (res.data)
      })
      .catch(err=>err) 
    },
    getSlug() {
      console.log(this.slug,'slug')
      this.$router.push(`city/${this.slug}`)
    }
  },
  mounted() {
    this.fetchCities();
  }
};
</script>

<style>
.image {
  min-height: 100%;
  min-width: 1024px;
  width: 100%;
  height: auto;
  position: fixed;
  top: 0;
  left: 0;
}

.haederImage {
  position: relative;
}

.searchFilterDiv {
  position: fixed;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  width: 100%;
  background: white;
  max-width: 100% !important;
  text-align: center;
  padding: 10px;
}
</style>

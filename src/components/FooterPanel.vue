<template>
  <footer class="mt-4">
    <p class="badge-pill badge-footer" v-for="render in content.body" :key="render.body">
      @{{render.year}} - {{render.publisher}}
      <br />
      <a class="mail" v-bind:href="['mailto:' + render.mail]">{{render.title}}</a>
    </p>
  </footer>
</template>

<script>
export default {
  name: 'App',

  data () {
    return {
      content: {
        body: [
          {
            publisher: 'Rizal Valry',
            year: '2020',
            mail: 'rizal.muh.rzl@gmail.com',
            title: 'Imdb Movie'
          }
        ]
      }
    }
  }
}
</script>

<style scoped>
a.mail {
  font-weight: 500;
  font-size: 5vh;
  text-decoration: none;
  color: black;
}

.badge-footer {
  color: rgb(250, 248, 248);
  background-color: transparent !important;
  text-shadow: 0 0 2px rgb(229, 253, 10);
}
</style>

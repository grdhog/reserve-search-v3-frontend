<script>
import { defineComponent } from 'vue'



export default defineComponent({
  name: 'App',
  components: {},
  mounted: function () {
    this.getItems();
  },
  data: {
    URL: 'http://54.252.3.209:8000/show-in-menus-login-required/',
    items: []
  },
  methods: {
    getItems: function () {
      console.log('calling getItems')
      var oReq = new XMLHttpRequest()
      var that = this;
      oReq.addEventListener('load', function () {
        var json = JSON.parse(this.responseText)
        that.items = json.data;
      })
      oReq.addEventListener('error', function () {
        console.error('API not working!')
      })
      oReq.open('GET', this.URL);
      oReq.send();
    },
  },
})
</script>

<template>
  <div id="pcc-show-in-menus">
    <div class="pcc-standard-body">
      <table>
      <thead>        
        <th>Name</th>
        <th>Suburb</th>
        <th>Primary Purpose</th>
      </thead>
      <tbody>
        <tr v-for="anchor in items">
          <td><a :href="anchor.url" target="_blank">{{ anchor.title }}</a></td>
          <td>{{ anchor.user }}</td>
          <td>{{ anchor.url }}</td>
        </tr>
      </tbody>
      </table>
    </div>
  </div>
</template>

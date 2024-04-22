<template>
  <Luisa :design="design" :config="config" v-model="viewModel"/>
</template>
<script>

// import app from './app.json'

export default {
  name: 'Start',
  data: function() {
    return {
      // design: app,
      design: "a2aa10a9RpVhDUsyPupJI1QMsxx0euPKJhDMDNuQz3CowVldyJNyIX3yb2bW",
      viewModel: {
        search_name:'',
        display_name: '',
        photo: ''
      },
      config: {
      },
    }
  },
  components: {
  },
  methods: {
    search () {
      let url = "https://api.github.com/users/" + this.viewModel.search_name

      fetch(url, {
        method: "GET"
      })
      .then((response) => {
        response.json().then((data) => {
          this.viewModel.display_name = "[User not found]"
          if (data.name != null) {
            this.viewModel.display_name = data.name;
            this.viewModel.photo = data.avatar_url;
          }
        });
      })
      .catch((err) => {
        console.error(err);
      });
    }
    // hello () {
    //   this.viewModel.welcome = "Hello " + this.viewModel.user_name
    //   this.viewModel.live = "."
    // },
    // liveUpdate () {
    //   this.viewModel.live = "Typing " + this.viewModel.user_name
    // }
  }
}
</script>
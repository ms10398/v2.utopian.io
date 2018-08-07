<script>
import ULayoutPage from 'src/layouts/parts/page/page'
import firebase from 'firebase/app'

export default {
  name: 'PageProjectContributors',
  components: {
    ULayoutPage
  },
  data () {
    return {
      loading: true,
      contributors: []
    }
  },
  methods: {
    async loadInitial () {
      this.loading = true
      const call = firebase.functions().httpsCallable(`/api/projects/contributors?q=${this.$route.params.name}`)
      await call()
        .then((result) => {
          this.contributors = result.data
        })
        .catch((err) => console.log(err))
      console.log(this.contributors)
    }
  },
  mounted () {
    this.loadInitial()
    return true
  }
}

</script>

<style lang="stylus" src="./contributors.styl"></style>

<template lang="pug" src="./contributors.pug"></template>

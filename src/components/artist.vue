<template lang="pug">
  li
    hr
    h2
        a(:href='artist.url' target="_blank") {{artist.name}}
        img(id='imagen' :src="artist.image[2]['#text']")
    
</template>

<script>
export default {
  name: 'artist',
  props: [ 'artist' ]
}
</script>

<style lang="stylus">
 a
    display flex
    justify-content center !important

 
</style>

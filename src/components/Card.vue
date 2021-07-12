<template>
  <p>
      titolo:{{details.title}} - titolo originale: {{details.original_title}} - Lingua: {{details.original_language}}- Voto: {{details.vote_average}}

  </p>
</template>

<script>
export default {
    name:'Card',
    props:['details']

}
</script>

<style>

</style>
<template>
  <b-btn id="newGame" block variant="primary" class="ml-2 mr-2" @click="$emit('newGame')">
    New Game
  </b-btn>
</template>

<script>
export default {
  name: 'NewGameButton',
};
</script>

<style scoped>
#newGame{
  width: 120px;
}
</style>

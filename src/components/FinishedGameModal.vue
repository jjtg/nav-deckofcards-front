<template>
  <b-modal v-model="displayFinishedState" title="The Game Is Over">
    The winner is: <b>{{winner.playerName}}</b><br>
    <span v-for="player in players" :key="player.playerName">
      {{player.playerName}} - {{player.score}} - {{player.handDisplay}} <br></span>
  </b-modal>
</template>

<script>
export default {
  name: 'FinishedGameModal',
  props: ['finished', 'winner', 'players'],
  data() {
    return {
      displayFinishedState: false,
    };
  },
  mounted() {
    this.displayFinishedState = this.finished;
  },
};
</script>

<style scoped>

</style>

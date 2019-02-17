<template>
  <div>
    <b-button :variant="buttonVariant" class="mr-3">
      {{player.playerName}}
      <b-badge :variant="badgeVariant">{{player.score}}</b-badge>
    </b-button>
  </div>
</template>

<script>
export default {
  name: 'PlayerBadge',
  props: ['winner', 'player'],
  computed: {
    buttonVariant() {
      if (this.winner == null) return 'light';
      if (this.winner.playerName === this.player.playerName) return 'success';
      return 'danger';
    },
    badgeVariant() {
      // eslint-disable-next-line
      const score = this.player.score;
      if (score === 21) return 'success';
      if (score > 21) return 'danger';
      if (score < 17) return 'info';
      return 'warning';
    },
  },
};
</script>

<style scoped>
</style>

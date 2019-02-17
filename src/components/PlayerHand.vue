<template>
  <b-col>
    <b-row>
      <div v-for="card in player.hand" :key="`${card.value}-${card.suit}`">
        <b-img class="mt-1 ml-1" thumbnail fluid
               :src="`${publicPath}images/${getCardAssetPath(card)}`"
               :alt="`${card.value} - ${card.suit}`"/>
      </div>
    </b-row>
  </b-col>
</template>

<script>
export default {
  name: 'PlayerHand',
  props: ['player'],
  data() {
    return {
      publicPath: process.env.BASE_URL,
    };
  },
  methods: {
    getCardAssetPath(card) {
      return `${card.value}_${card.suit}.png`;
    },
  },
};
</script>

<style scoped>
</style>

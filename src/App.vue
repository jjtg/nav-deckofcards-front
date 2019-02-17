<template>
  <div id="app">
    <div id="background">
      <b-container v-if="gameState" class="table">
        <b-row class="player" v-for="(player, i) in state.users" :key="`${i}-user`">
          <b-col sm="2"/>
          <player-badge :winner="state.winner" :player="player"/>
          <player-hand :player="player"></player-hand>
          <b-col sm="2"/>
        </b-row>
        <b-row>
          <b-col/>
          <b-col><continue-button :finished="state.finished" @continueGame="continueGame"/>
          </b-col>
          <b-col><new-game-button @newGame="fetchNewGameState"/></b-col>
          <b-col/>
        </b-row>
      </b-container>
      <finished-game-modal
        v-if="gameState && gameState.gameState.finished"
        :finished="state.finished"
        :players="state.users"
        :winner="state.winner"/>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import PlayerHand from './components/PlayerHand.vue';
import PlayerBadge from './components/PlayerBadge.vue';
import ContinueButton from './components/ContinueButton.vue';
import NewGameButton from './components/NewGameButton.vue';
import FinishedGameModal from './components/FinishedGameModal.vue';
import constants from './utilities/constants';

export default {
  name: 'app',
  components: {
    ContinueButton,
    NewGameButton,
    PlayerHand,
    PlayerBadge,
    FinishedGameModal,
  },
  data() {
    return {
      gameState: null,
      publicPath: process.env.BASE_URL,
    };
  },
  computed: {
    state() {
      if (this.gameState) return this.gameState.gameState;
      return null;
    },
  },
  methods: {
    fetchNewGameState() {
      axios.get(`${constants.rootUrl}/blackjack`)
        .then((res) => { this.gameState = res.data; })
        // eslint-disable-next-line no-console
        .catch(console.error);
    },
    continueGame() {
      axios.post(`${constants.rootUrl}/blackjack`, this.gameState)
        .then((res) => { this.gameState = res.data; })
        // eslint-disable-next-line no-console
        .catch(console.error);
    },
  },
  mounted() {
    this.fetchNewGameState();
  },
};
</script>

<style src="./css/app.css"></style>

<template>
  <b-btn id="continueGame"
         :disabled="finished"
         block class="ml-2 mr-2"
         :variant="buttonVariant"
         @click="continueGame">
    Continue
  </b-btn>
</template>

<script>
export default {
  name: 'ContinueButton',
  props: ['finished'],
  computed: {
    buttonVariant() {
      if (!this.finished) return 'primary';
      return '';
    },
  },
  methods: {
    continueGame() {
      if (!this.finished) this.$emit('continueGame');
    },
  },
};
</script>

<style scoped>
#continueGame{
  width: 120px;
}
</style>

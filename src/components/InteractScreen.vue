<template>
  <div>
    <p>Màn hình interact</p>
    <card-filed
      v-for="(card, index) in cardsContext"
      :key="index"
      :imgBackFaceUrl="`images/${card}.png`"
    />
  </div>
</template>

<script>
import CardFiled from "./CardFiled.vue";
export default {
  components: { CardFiled },
  props: {
    cardsContext: {
      type: Array,
      default: function () {
        return [];
      },
    },
  },
};
</script>

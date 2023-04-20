<template>
  <div
    class="interct-screen"
    :class="{
      column4x4: cardsContext.length / 4 == 4,
      column6x6: cardsContext.length / 6 == 6,
      column8x8: cardsContext.length / 8 == 8,
      column10x10: cardsContext.length / 10 == 10,
    }"
  >
    <card-filed
      v-for="(card, index) in cardsContext"
      :key="index"
      :imgBackFaceUrl="`images/${card}.png`"
      :card="{ index, value: card }"
      :ref="`card-${index}`"
      :rules="rules"
      @onFlip="checkRules($event)"
    />
  </div>
</template>

<script>
import CardFiled from "./CardFiled.vue";
// import ref from "vue";
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
  data() {
    return {
      rules: [],
      countSuccess: 0,
    };
  },
  methods: {
    checkRules(card) {
      this.rules.push(card);
      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        //chọn đúng: add class disabled tới component Card
        this.$refs[`card-${this.rules[0].index}`][0].onDisable();
        this.$refs[`card-${this.rules[1].index}`][0].onDisable();
        // reset rules
        this.rules = [];
        this.countSuccess += 1;
        if (this.countSuccess === this.cardsContext.length / 2) {
          const date = new Date();
          this.$emit("onFinish", date.getTime());
        }
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        setTimeout(() => {
          // chọn sai: hiển thị mặt front
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          // reset rules
          this.rules = [];
        }, 600);
      } else return false;
    },
  },
};
</script>
<style scoped>
.interct-screen {
  width: 100vw;
  min-height: 100vh;
  height: auto;
  background-color: var(--black);
  display: grid;
  padding: 10px;
  justify-content: center;
  align-content: center;
}

.column4x4 {
  grid-template-columns: 140px 140px 140px 140px;
}
.column6x6 {
  grid-template-columns: 140px 140px 140px 140px 140px 140px;
}
.column8x8 {
  grid-template-columns: 140px 140px 140px 140px 140px 140px 140px 140px;
}
.column10x10 {
  grid-template-columns: 140px 140px 140px 140px 140px 140px 140px 140px 140px 140px;
}
</style>

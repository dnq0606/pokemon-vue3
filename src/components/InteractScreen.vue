<template>
  <div>
    <card-filed
      v-for="(card, index) in cardsContext"
      :key="index"
      :imgBackFaceUrl="`images/${card}.png`"
      :card="{ index, value: card }"
      :ref="`card-${index}`"
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
    };
  },
  methods: {
    checkRules(card) {
      if (this.rules.length === 2) return false;
      this.rules.push(card);

      if (
        this.rules.length === 2 &&
        this.rules[0].value === this.rules[1].value
      ) {
        console.log("ok");
      } else if (
        this.rules.length === 2 &&
        this.rules[0].value !== this.rules[1].value
      ) {
        setTimeout(() => {
          this.$refs[`card-${this.rules[0].index}`][0].onFlipBackCard();
          this.$refs[`card-${this.rules[1].index}`][0].onFlipBackCard();
          this.rules = [];
        }, 800);
      } else return false;
    },
  },
  // setup() {
  //   let card-${this.rules[0].index} = ref(null);

  //   const handleClick = () => {
  //     myButtonRef.value.innerHTML = "Clicked!";
  //   };

  //   return {
  //     handleClick,
  //     myButtonRef,
  //     myComponentRef,
  //   };
  // },
};
</script>

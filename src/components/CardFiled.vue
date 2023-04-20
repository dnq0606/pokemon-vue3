<template>
  <div class="card" :class="{ disabled: isDisabled }">
    <div
      class="card__inner"
      :class="{ 'is-flipped': isFiled }"
      @click="onToggleFiledCard"
    >
      <div class="card__face card__face--front">
        <div class="card__content"></div>
      </div>
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url(${require('@/assets/' + imgBackFaceUrl)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardFiled",
  data() {
    return {
      isFiled: false,
      isDisabled: false,
    };
  },
  props: {
    imgBackFaceUrl: {
      type: String,
      require: true,
    },
    card: {
      type: [String, Number, Array, Object],
    },
    rules: {
      type: Array,
    },
  },
  methods: {
    onToggleFiledCard() {
      if (this.rules.length >= 2) return false;
      if (this.isDisabled) return false;
      this.isFiled = !this.isFiled;
      if (this.rules.length === 2) return false;
      if (this.isFiled) this.$emit("onFlip", this.card);
    },
    onFlipBackCard() {
      this.isFiled = false;
    },
    onDisable() {
      this.isDisabled = true;
    },
  },
};
</script>

<style lang="css" scoped>
.card {
  display: inline-block;
  margin-right: 1rem;
  padding: 1rem;
  width: 140px;
  height: 160px;
}

.card__inner {
  width: 100%;
  height: 100%;
  transition: 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}
.card__inner.is-flipped {
  transform: rotateY(-180deg);
}
.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.4);
}

.card__face--front .card__content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  background-size: 40px 40px;
  width: 100%;
  height: 100%;
}

.card__face--back {
  /* background-color: var(--black) ; */
  transform: rotateY(-180deg);
}
.card__face--back .card__content {
  background-size: contain;
  background-position: center;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
}

.card.disabled .card__inner {
  cursor: default;
}
</style>

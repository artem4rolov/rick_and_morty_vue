<template>
  <div class="card">
    <div class="card__header">
      <div class="header__left">
        <div class="name">{{ char.name }}</div>
        <div class="gender">{{ char.gender }}</div>
      </div>
      <div class="header__right">
        <div class="origin">{{ char.origin.name }}</div>
        <div class="status">{{ char.status }}</div>
      </div>
    </div>
    <img :src="char.image" alt="character image" class="card__avatar" />
  </div>
</template>

<script>
export default {
  name: "CharCard",
  props: ["char"],
  mounted() {
    this.getChar();
  },
  methods: {
    getChar() {
      if (this.char) {
        console.log(this.char);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card {
  width: 300px;
  height: 318px;
}
.card__header {
  display: flex;
  justify-content: space-between;
}

.header__left {
  display: flex;
  flex-direction: column;
  text-align: left;
  align-items: start;
}

.header__right {
  display: flex;
  flex-direction: column;
  align-items: end;
}
</style>

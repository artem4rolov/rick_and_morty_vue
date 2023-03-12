<template>
  <div class="card">
    <div class="card__header">
      <div class="header__left">
        <div class="name">{{ char.name }}</div>
        <div class="gender">{{ char.gender }}</div>
      </div>
      <div class="header__right">
        <div class="status" :class="aliveClass">{{ char.status }}</div>
        <div class="origin">{{ char.origin.name }}</div>
      </div>
    </div>
    <img :src="char.image" alt="character image" class="card__avatar" />
  </div>
</template>

<script>
export default {
  name: "CharCard",
  props: ["char"],
  data() {
    return {
      aliveClass:
        this.char.status === "Alive"
          ? "alive"
          : this.char.status === "Dead"
          ? "dead"
          : "",
    };
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

.name {
  color: #333333;
  font-size: 12px;
  line-height: 14px;
  font-weight: 700;
}

.gender,
.origin {
  color: #8d8d8d;
  font-size: 12px;
  line-height: 14px;
  font-weight: 400;
}

.status {
  color: #8d8d8d;
  font-size: 12px;
  line-height: 14px;
  font-weight: 700;
}

.alive {
  color: #00bd4c;
}

.dead {
  color: #e60000;
}
</style>

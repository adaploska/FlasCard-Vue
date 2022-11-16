<template>
  <div class="cardItem">
    <div class="card" :class="{ active: active_el === card.id }">
      <div class="card__face card__face--front" @click="activate(card.id)">
        <div class="header">
          <img
            @click="removeCard(card.id)"
            alt="remove logo"
            src="@/assets/delete.svg"
            width="20"
            height="20"
          />
        </div>
        <img
          class="questionImg"
          alt="question mark logo"
          src="@/assets/question-mark.svg"
          width="75"
        />
        <div class="title">{{ card.question }}</div>
        <ul>
          <li
            v-for="answer in card.answers"
            v-bind:key="answer"
            :answer="answer"
          >
            {{ answer }}
          </li>
        </ul>
      </div>
      <div class="card__face card__face--back" @click="returnToFont(card.id)">
        {{ card.correctAnswer }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardVue",
  props: {
    card: Object,
  },
  data() {
    return {
      active_el: 0,
    };
  },

  methods: {
    activate: function (el) {
      this.active_el = el;
    },
    returnToFont: function () {
      this.active_el = 0;
    },
    removeCard(id) {
      this.$emit("deleteTrigger", id);
    },
  },
};
</script>

<style lang="scss">
.header {
  display: flex;
  flex-direction: row;
  justify-content: end;
  margin-right: 15px;
}
.questionImg {
  margin: 0 auto;
}
.cardItem {
  height: 350px;
  position: relative;
  ul {
    padding: 0;
    li {
      list-style-type: none;
    }
  }
}

.card {
  position: relative;
  width: 100%;
  height: 100%;
  cursor: pointer;
  transform-style: preserve-3d;
  transform-origin: center right;
  transition: transform 1s;
  text-align: center;
}

.card.active {
  transform: translateX(-100%) rotateY(-180deg);
}

.card__face {
  position: absolute;
  width: 100%;
  height: 100%;
  color: white;
  text-align: center;
  font-weight: bold;
  backface-visibility: hidden;
  display: flex;
  box-shadow: 6px 6px 26px -6px #1f2124;
  flex-direction: column;
  justify-content: space-around;
}

.card__face--front {
  background: #2d7f70;
  border-radius: 27px 7px 27px 7px;

  .title {
    font-size: 25px;
    color: white;
  }
}

.card__face--back {
  background: #40b59f;
  transform: rotateY(180deg);
  color: black;
  position: absolute;
  text-align: center;
  font-size: 18px;
  border-radius: 27px 7px 27px 7px;
}
</style>

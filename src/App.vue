<template>
  <h1>FlashCards</h1>
  <div class="grid">
    <SearchCard @searchCards="searchCards" />
    <AddCard @addCard="addCard" />
    <div class="buttons">
      <ShuffleCard @shuffleCard="shuffle" />
      <ResetShuffleCard @resetShuffle="resetShuffle" />
    </div>
  </div>
  <div class="cardsWrapper">
    <Card
      v-for="card in filteredCards"
      :key="card.id"
      :card="card"
      @deleteTrigger="deleteCard"
    />
  </div>
</template>

<script>
import Card from "./components/Card.vue";
import AddCard from "./components/AddCard.vue";
import ShuffleCard from "./components/ShuffleCard.vue";
import ResetShuffleCard from "./components/ResetShuffle.vue";
import SearchCard from "./components/SearchCard.vue";
export default {
  name: "App",
  components: {
    Card,
    AddCard,
    ShuffleCard,
    ResetShuffleCard,
    SearchCard,
  },
  data() {
    return {
      cards: [
        {
          id: 1,
          question: "Harvard University is located in which city? ",
          answers: ["New York", "Washington D.C.", "Cambridge", "Providence"],
          correctAnswer: "Cambridge ",
        },
        {
          id: 2,
          question:
            "The Republic of Malta is the smallest microstate worldwide.",
          answers: ["True", "False"],
          correctAnswer: "False",
        },
        {
          id: 3,
          question: "What is the largest organ of the human body?",
          answers: ["Heart", "large Intestine", "Liver", "Skin"],
          correctAnswer: "Skin",
        },
        {
          id: 4,
          question: "Tokyo is the capital of Japan.",
          answers: ["True", "False"],
          correctAnswer: "True",
        },
        {
          id: 5,
          question: "The Space Needle is located in which city?",
          answers: ["Los Angles", "Toronto", "Vancouver", "Seattle"],
          correctAnswer: "Seattle",
        },
      ],
      active_el: 0,
      search: "",
    };
  },
  methods: {
    deleteCard(id) {
      this.cards = this.cards.filter((card) => card.id !== id);
    },
    addCard(newCard) {
      this.cards.push(newCard);
      console.log(this.cards);
    },
    shuffle() {
      let cards = [...this.cards];
      let first,
        second,
        temp,
        count = cards.length;
      for (let i = 0; i < 10; i++) {
        first = Math.floor(Math.random() * count);
        second = Math.floor(Math.random() * count);
        temp = cards[first];
        cards[first] = cards[second];
        cards[second] = temp;
      }
      this.cards = cards;
    },
    resetShuffle() {
      this.cards.sort(function (a, b) {
        return a.id - b.id;
      });
    },
    searchCards(keyword) {
      console.log(keyword);
      this.search = keyword;
    },

    mounted() {
      this.deleteCard();
      this.shuffle();
      this.addCard();
      this.resetShuffle();
    },
  },
  computed: {
    filteredCards() {
      return this.cards.filter((card) => {
        return card.question
          .toLowerCase()
          .includes(this.search.trim().toLowerCase());
      });
    },
  },
};
</script>

<style lang="scss">
body {
  background: gray;
  height: 100%;
  color: white;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: gray;
}
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  grid-gap: 35px;
  input {
    border-radius: 7px;
    height: 35px;
    font-size: 25px;
    margin: 10px;
  }
  .buttons {
    display: flex;
    flex-direction: column;
    padding: 20px;
    border-radius: 7px;
    margin-top: 105px;
  }
}
.cardsWrapper {
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  grid-gap: 35px;
  margin-top: 50px;
}
</style>

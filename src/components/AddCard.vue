<template>
  <div class="addwrapper">
    <p>Add new Card</p>
    <form @submit.prevent="addCard()">
      <input v-model="question" placeholder="Question" />

      <input v-model="answers" placeholder="answer1, answer2" />

      <input v-model="correctAnswer" placeholder="Correct answer" />
      <div class="error">{{ error && error }}</div>
      <button class="addButton">Add</button>
    </form>
  </div>
</template>
<script>
export default {
  name: "AddCard",
  props: {},
  data() {
    return {
      question: "",
      answers: [],
      correctAnswer: "",
      id: 6,
      error: "",
    };
  },

  methods: {
    addCard() {
      if (
        this.question === "" ||
        this.answers === [] ||
        this.correctAnswer === ""
      ) {
        this.error = "Enter all input";
      } else {
        const newCard = {
          id: this.id++,
          question: this.question,
          answers: this.answers.split(/[ ,]+/),
          correctAnswer: this.correctAnswer,
        };
        this.$emit("addCard", newCard);
        this.error = "";
        this.question = "";
        this.answers = "";
        this.correctAnswer = "";
      }
    },
  },
};
</script>
<style lang="scss">
.addwrapper {
  display: flex;
  flex-direction: column;
  border: 5px solid #2d7f70;
  padding: 20px;
  border-radius: 27px 7px 27px 7px;
  p {
    font-size: 25px;
  }
  .error {
    color: red;
  }
  .addButton {
    display: block;
    background: #40b59f;
    color: white;
    padding: 15px 20px;
    margin: 10px 10px;
    border-radius: 5px;
    text-decoration: none;
    border: none;
    font-size: 25px;
    &:hover {
      background: #2d7f70;
    }
  }
}
</style>

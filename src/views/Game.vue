<template>
  <header>
    <h1>{{ message }}</h1>
    <p class="between">(btn 1 and 20)</p>
    <button class="btn restart" @click="restartGame">Play Again</button>
    <div class="number">{{ showSecretNumber ? secretNumber : "?" }}</div>
  </header>
  <main>
    <section class="left">
      <input type="number" class="guess" v-model="userGuess" />
      <button class="btn check" @click="checkGuess">Check!</button>
    </section>
    <section class="right">
      <p class="message">{{ message }}</p>
      <p class="label-score">
        💯 Score: <span class="score">{{ score }}</span>
      </p>
      <p class="label-highscore">
        👑 Highscore: <span class="highscore">{{ highscore }}</span>
      </p>
    </section>
  </main>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const secretNumber = ref(Math.trunc(Math.random() * 20) + 1);
    const score = ref(20);
    const message = ref("");
    const userGuess = ref("");

    const checkGuess = () => {
      const guess = Number(userGuess.value);

      if (!guess) {
        message.value = "⛔ No Number!";
      } else if (guess === secretNumber.value) {
        message.value = "🎉 Correct Number.";
        document.body.style.backgroundColor = "#60b347";
      } else if (guess > secretNumber.value) {
        if (score.value > 1) {
          message.value = "📈 Too high!";
          score.value--;
        } else {
          message.value = "☹ You lost the game!";
          score.value = 0;
        }
      } else if (guess < secretNumber.value) {
        if (score.value > 1) {
          message.value = "📉 Too low!";
          score.value--;
        } else {
          message.value = "☹ You lost the game!";
          score.value = 0;
        }
      }
    };

    const restartGame = () => {
      score.value = 20;
      secretNumber.value = Math.trunc(Math.random() * 20) + 1;
      message.value = "Start guessing...";
      userGuess.value = "";
      document.body.style.backgroundColor = "#b2beb5";
    };

    return {
      message,
      score,
      userGuess,
      checkGuess,
      restartGame,
    };
  },
};
</script>

<style></style>

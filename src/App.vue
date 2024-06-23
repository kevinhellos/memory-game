<script>
export default {
  name: "App",

  data() {
    return {
      fruits: [
        { id: 1, photoUrl: "/assets/fruits/apple.png", isShown: false, matched: false },
        { id: 2, photoUrl: "/assets/fruits/banana.png", isShown: false, matched: false },
        { id: 3, photoUrl: "/assets/fruits/guava.png", isShown: false, matched: false },
        { id: 4, photoUrl: "/assets/fruits/kiwi.png", isShown: false, matched: false },
        { id: 5, photoUrl: "/assets/fruits/lemon.png", isShown: false, matched: false },
        { id: 6, photoUrl: "/assets/fruits/orange.png", isShown: false, matched: false },
        { id: 7, photoUrl: "/assets/fruits/pineapple.png", isShown: false, matched: false },
        { id: 8, photoUrl: "/assets/fruits/strawberry.png", isShown: false, matched: false },
        { id: 9, photoUrl: "/assets/fruits/apple.png", isShown: false, matched: false },
        { id: 10, photoUrl: "/assets/fruits/banana.png", isShown: false, matched: false },
        { id: 11, photoUrl: "/assets/fruits/guava.png", isShown: false, matched: false },
        { id: 12, photoUrl: "/assets/fruits/kiwi.png", isShown: false, matched: false },
        { id: 13, photoUrl: "/assets/fruits/lemon.png", isShown: false, matched: false },
        { id: 14, photoUrl: "/assets/fruits/orange.png", isShown: false, matched: false },
        { id: 15, photoUrl: "/assets/fruits/pineapple.png", isShown: false, matched: false },
        { id: 16, photoUrl: "/assets/fruits/strawberry.png", isShown: false, matched: false }
      ],
      flippedCards: [],
      score: 0,
      noOfClicks: 0,
    };
  },

  created() {
    this.shuffleFruits();
  },

  methods: {
    flipCard(fruit) {
      this.noOfClicks ++;
      if (this.flippedCards.length < 2 && !fruit.isShown && !fruit.matched) {
        fruit.isShown = true;
        this.flippedCards.push(fruit);

        if (this.flippedCards.length === 2) {
          setTimeout(this.checkMatch, 500);
        }
      }
    },

    checkMatch() {
      const [card1, card2] = this.flippedCards;
      if (card1.photoUrl === card2.photoUrl) {
        card1.matched = card2.matched = true;
        this.score += 1;
      } 
      else {
        card1.isShown = card2.isShown = false;
      }
      this.flippedCards = [];
    },

    shuffleFruits() {
      for (let i = this.fruits.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [this.fruits[i], this.fruits[j]] = [this.fruits[j], this.fruits[i]];
      }
    }
  }
};
</script>

<template>
  <div class="text-center mb-8 mt-12">
    <h1 class="text-3xl mb-3">Memory Game</h1>
    <h3 
      class="font-bold text-xl mb-3 font-sans"
      v-if="score == 8"
      >
      ✅ <span class="text-green-600">Completed</span> with {{ noOfClicks }} clicks
    </h3>
    <div class="bg-gray-50 w-[410px] text-gray-600 mx-auto p-3 rounded-md">
      Click on the card to reveal the image <br>
      You can only open 2 cards at once
    </div>
  </div>
  <div class="flex justify-center items-center">
    <div class="grid grid-cols-4 gap-4">
      <button 
        v-for="fruit in fruits" :key="fruit.id"
        class="border border-gray-200 w-24 h-24 bg-slate-100 hover:bg-slate-200 rounded-xl p-5 text-center shadow-sm"
        @click="flipCard(fruit)"
      >
        <img 
          v-if="fruit.isShown || fruit.matched"
          :src="fruit.photoUrl" 
          width="110" 
        />
      </button>
    </div>    
  </div>
</template>

<style scoped>
.grid {
  max-width: 400px;
}
</style>
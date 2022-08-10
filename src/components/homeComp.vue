<template>
  <body class="antialiased text-gray-700">
    <div class="pt-0 flex w-full h-screen justify-center item-center">
      <div class="pt-0 w-full max-h-xl">
        <h1 class="pt-0 font-bold text-5xl text-center text-indigo-700">
          simple Quiz
        </h1>

        <div class="bg-white shadow-2xl rounded-lg p-12 w-auto mt-8">
          <div v-if="count != -1">
            <p class="text-2xl font-bold">{{ question[index].question }}</p>
            <label
              :for="key"
              v-for="(option, key) in question[index].options"
              :key="key"
              v-bind:class="
                ({
                  'hover:bg-gray-100 cursor-pointer':
                    slectedAnswer != '' || true,
                },
                { 'bg-red-200': slectedAnswer == key },
                {
                  'bg-green-200':
                    key == question[index]['correctAnswer'] &&
                    slectedAnswer != '',
                })
              "
              class="block mt-4 border border-gray-300 rounded-lg py-2 px-6 text-lg"
            >
              <input
                type="radio"
                :id="key"
                class="hidden"
                :value="key"
                @change="answered($event)"
                v-model="slectedAnswer"
                :disabled="slectedAnswer != ''"
              />
              {{ option }}
            </label>
            <div class="mt-6 flow-root">
              <button
                @click="next()"
                class="float-right bg-indigo-700 px-6 py-2 text-white font-bold rounded-lg"
                v-show="slectedAnswer != '' && count != 0"
              >
                Next
              </button>
              <button
                @click="result()"
                class="float-right bg-indigo-700 px-6 py-2 text-white font-bold rounded-lg"
                v-show="slectedAnswer != '' && count == 0"
              >
                Finish
              </button>
            </div>
          </div>
          <div v-else>
            <h1 class="text-bold text-3xl text-indigo-50">Result</h1>

            <div class="flex justify-start space-x-4 mt-6">
              <p>
                Correct answer:
                <span class="text-2xl text-green-700 font-bold">{{
                  correct
                }}</span>
              </p>
              <p>
                Wrong answer:
                <span class="text-2xl text-red-700 font-bold">{{ wrong }}</span>
              </p>
            </div>
          </div>
          <button
            @click="playagain()"
            class="float-right bg-indigo-700 px-6 py-2 text-white font-bold rounded-lg"
            v-show="finish"
          >
            Play Again
          </button>
        </div>
      </div>
    </div>
  </body>
</template>

<script>
export default {
  name: "homeComp",

  data() {
    return {
      key: "",
      finish: false,
      correct: 0,
      wrong: 0,
      count: 2,
      index: 0,
      any: true,
      slectedAnswer: "",
      question: [
        {
          question:
            "Rolex is a company that specializes in what type of product?",
          options: { a: "Bags", b: "Watches", c: "Shoes", d: "Laptops" },
          correctAnswer: "b",
        },
        {
          question: "When did Facebook launch?",
          options: { a: "2005", b: "2008", c: "2003", d: "2004" },
          correctAnswer: "d",
        },
        {
          question:
            "Albert Einstein had trouble with mathematics when he was in school",
          options: { a: "True", b: "False" },
          correctAnswer: "b",
        },
      ],
    };
  },
  methods: {
    answered(e) {
      this.slectedAnswer = e.target.value;
      if (this.slectedAnswer == this.question[this.index].correctAnswer) {
        this.correct++;
      } else {
        this.wrong++;
      }
    },
    next() {
      this.index++;
      this.count--;
      console.log(this.slectedAnswer);
      console.log(this.key);

      this.slectedAnswer = "";
    },
    result() {
      this.count = -1;
      this.finish = true;
    },
    playagain() {
      this.finish = false;
      this.correct = 0;
      this.wrong = 0;
      this.count = 2;
      this.index = 0;
      this.slectedAnswer = "";
    },
  },
};
</script>

<script>
import { reactive, computed } from "vue";

export default {
  setup() {
    const state = reactive({
      user: {
        name: "Leye",
        email: "oladipo@gmail.com",
      },
      email: "",
      password: "",
      questions: [
        {
          question: "Which language runs in a web browser?",
          options: ["Java", "C", "Python", "JavaScript"],
          correctAnswer: 3,
        },
        {
          question: "What does CSS stand for?",
          options: [
            "Central Style Sheets",
            "Cascading Style Sheets",
            "Cascading Simple Sheets",
            "Cars SUVs Sailboats",
          ],
          correctAnswer: 1,
        },
        {
          question: "What does HTML stand for?",
          options: [
            "Hypertext Markup Language",
            "Hypertext Markdown Language",
            "Hyperloop Machine Language",
            "Helicopters Terminals Motorboats Lamborghinis",
          ],
          correctAnswer: 0,
        },
        {
          question: "What year was JavaScript launched?",
          options: ["1996", "1995", "1994", "None of the above"],
          correctAnswer: 1,
        },
      ],
      currentQuestionIndex: 0,
      selectedAnswer: null,
      score: 0,
      showResults: false,
    });

    const currentQuestion = computed(() => state.questions[state.currentQuestionIndex]);
    const isLastQuestion = computed(() => state.currentQuestionIndex === state.questions.length - 1);

    const selectAnswer = (index) => {
      state.selectedAnswer = index;
    };

    const submitAnswer = () => {
      if (state.selectedAnswer === currentQuestion.value.correctAnswer) {
        state.score++;
      }

      if (isLastQuestion.value) {
        state.showResults = true;
      } else {
        state.currentQuestionIndex++;
        state.selectedAnswer = null;
      }
    };

    const goBack = () => {
      if (state.currentQuestionIndex > 0) {
        state.currentQuestionIndex--;
        state.selectedAnswer = null;
      }
    };

    const reloadQuiz = () => {
      state.currentQuestionIndex = 0;
      state.selectedAnswer = null;
      state.score = 0;
      state.showResults = false;
    };

    return {
      state,
      currentQuestion,
      isLastQuestion,
      selectAnswer,
      submitAnswer,
      goBack,
      reloadQuiz,
    };
  },
};
</script>

<template>
  <section class="bg-[#3F0DC5] h-screen overflow-hidden items-center">
    <div v-if="!state.showResults">
      <div class="flex justify-center items-center px-10 py-10">
        <div>
          <img src="/public/images/fingerprint.png" alt="" class="rounded-[60px] w-[576px] rounded-r-none" />
        </div>
        <div class="bg-white rounded-2xl px-[80px] py-[63px] relative rounded-l-none">
          <div class="bg-[#211E2A] flex justify-between text-white text-sm absolute top-[-2px] left-0 right-0 py-5 px-6 rounded-2xl rounded-l-none rounded-b-none">
            <span class="text-xs">Name: {{ state.user.name }}</span>
            <span class="text-xs">Email: {{ state.user.email }}</span>
          </div>
          <div class="flex justify-between pt-8">
            <button
              class="bg-[#F5F3FC] text-[#101828] p-3"
              :disabled="state.currentQuestionIndex === 0"
              @click="goBack"
            >
              Back
            </button>
            <img src="/images/checkbox.png" alt="" class="w-fit" />
            <span class="text-[#101828]">{{ state.currentQuestionIndex + 1 }} of {{ state.questions.length }}</span>
          </div>
          <div>
            <h1 class="text-[#101828] font-bold text-2xl pt-8">{{ currentQuestion.question }}</h1>
            <div
              v-for="(option, index) in currentQuestion.options"
              :key="index"
              :class="[ 
                'mt-4 rounded-2xl w-[400px] py-4 pl-3 border', 
                state.selectedAnswer === index ? 'bg-[#3F0DC5] text-white' : 'text-[#101828] border-[#101828] hover:bg-[#F5F3FC] hover:border-[#3F0DC5]'
              ]"
            >
              <button class="w-full text-left" @click="selectAnswer(index)">
                {{ option }}
              </button>
            </div>
            <button
              class="flex justify-center w-[400px] py-4 bg-[#3F0DC5] mt-4 rounded-2xl text-white hover:bg-[#3e0dc5da]"
              :disabled="state.selectedAnswer === null"
              @click="submitAnswer"
            >
              {{ isLastQuestion ? 'View Results' : 'Next' }}
            </button>
          </div>
        </div>
      </div>
    </div>

    <div v-if="state.showResults" class="flex justify-center items-center px-10 py-24">
      <div class="bg-white rounded-2xl px-[80px] py-[63px] relative rounded-l-none">
        <div class="bg-[#211E2A] flex justify-between text-white text-sm absolute top-[-2px] left-0 right-0 py-5 px-6 rounded-2xl rounded-l-none rounded-b-none">
          <span class="text-xs">Name: {{ state.user.name }}</span>
          <span class="text-xs">Email: {{ state.user.email }}</span>
        </div>

        <div class="flex justify-center flex-col my-10">
          <img src="/public/images/QA.png" alt="Quiz Results" class="w-full" />
          <p class="text-[#101828] font-bold mt-4">
            You answered {{ state.score }} out of {{ state.questions.length }} questions correctly
          </p>
          <button
            class="flex text-white bg-[#3F0DC5] justify-center mt-4 py-2 rounded-2xl"
            @click="reloadQuiz"
          >
            Reload!
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

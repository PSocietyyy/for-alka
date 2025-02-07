<script setup>
import { ref, onMounted, onUnmounted } from "vue";
import confetti from "canvas-confetti";

// Parallax Manual
const scrollY = ref(0);
const handleScroll = () => {
  scrollY.value = window.scrollY * 0.3;
};

// Countdown Valentine
const daysLeft = ref(0);
const updateCountdown = () => {
  const valentineDate = new Date(new Date().getFullYear(), 1, 14);
  const today = new Date();
  const timeDiff = valentineDate - today;
  daysLeft.value = Math.ceil(timeDiff / (1000 * 60 * 60 * 24));
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
  updateCountdown();
});

onUnmounted(() => {
  window.removeEventListener("scroll", handleScroll);
});

// Quotes Romantis
const quotes = ref([
  "“Cinta bukan hanya tentang memiliki, tapi tentang memahami.”",
  "“Kita mungkin tidak sempurna, tapi cinta kita bisa membuat segalanya lebih indah.”",
  "“Dalam kebisuanmu, aku masih mendengar detak hatimu yang membuatku tenang.”",
  "“Cinta sejati adalah ketika dua jiwa saling menemukan, bukan karena sempurna, tapi karena menerima ketidaksempurnaan.”",
  "“Di dunia yang penuh ketidakpastian, satu hal yang pasti adalah perasaanku padamu.”",
]);

// Status Surat
const isLetterOpened = ref(false);
const secretCounter = ref(0);
const showSecretMessage = ref(false);
const letterSlide = ref(0);

const openLetter = () => {
  isLetterOpened.value = true;
  confetti({ particleCount: 150, spread: 70, origin: { y: 0.6 } });
};

const nextSlide = () => {
  if (letterSlide.value < 7) {
    letterSlide.value++;
  }
};

const prevSlide = () => {
  if (letterSlide.value > 0) {
    letterSlide.value--;
  }
};

// Scroll ke bawah buat pesan terakhir
const showFinalMessage = ref(false);
const checkScrollToBottom = () => {
  if (window.innerHeight + window.scrollY >= document.body.offsetHeight) {
    showFinalMessage.value = true;
  }
};

// Tombol Rahasia
const handleSecretClick = () => {
  secretCounter.value++;
  if (secretCounter.value >= 5) {
    showSecretMessage.value = true;
  }
};

onMounted(() => {
  window.addEventListener("scroll", checkScrollToBottom);
});

onUnmounted(() => {
  window.removeEventListener("scroll", checkScrollToBottom);
});

// Tombol Tidak yang Mengecil
const isNoClicked = ref(false);
const handleNoClick = () => {
  if (!isNoClicked.value) {
    isNoClicked.value = true;
  }
};

// Tombol Ya
const handleYesClick = () => {
  alert("Kamu memilih Ya! 💖");
};

// Ganti Panggilan
const callNames = ref(["Alka", "JieJie"]);
const currentCallName = ref(callNames.value[0]);

const changeCallName = () => {
  const currentIndex = callNames.value.indexOf(currentCallName.value);
  const nextIndex = (currentIndex + 1) % callNames.value.length;
  currentCallName.value = callNames.value[nextIndex];
};

// Kalimat Penyesalan
const regretMessages = ref([
  "Aku benar-benar menyesal, Alka. Aku tahu aku telah melukai hatimu. Maafkan aku.",
  "Kehilanganmu adalah hal terburuk yang pernah terjadi padaku. Aku berharap bisa memperbaikinya.",
  "Aku tahu aku telah membuat kesalahan besar. Aku berjanji akan belajar dari kesalahanku.",
  "Aku berharap bisa kembali memperbaiki semua yang telah rusak antara kita.",
  "Alka, aku ingin kamu tahu betapa menyesalnya aku telah membuatmu merasa seperti itu.",
  "Setiap hari aku merenung, berharap bisa memperbaiki semuanya dan mengembalikan kebahagiaan kita.",
  "Aku Seharusnya tidak mempermasalahkan hobimu, karena itu merupakan bagian dari siapa dirimu.",
  "Aku hanya ingin tahu... apakah aku masih bisa masuk ke dalam duniamu lagi? 💌",
]);
</script>

<template>
  <div
    class="min-h-screen bg-gradient-to-r from-pink-400 to-purple-600 text-white font-sans overflow-hidden relative"
  >
    <!-- Background Gradient Bergerak -->
    <div class="absolute inset-0 bg-gradient-animation z-0"></div>

    <!-- Balon Cinta Melayang -->
    <div
      v-for="n in 30"
      :key="n"
      class="absolute bottom-0 left-0 w-full h-full pointer-events-none"
    >
      <div
        class="absolute bg-pink-300 rounded-full opacity-80 animate-float"
        :style="{
          width: `${Math.random() * 15 + 15}px`,
          height: `${Math.random() * 20 + 20}px`,
          left: `${Math.random() * 100}%`,
          animationDelay: `${Math.random() * 5}s`,
          animationDuration: `${Math.random() * 7 + 5}s`,
        }"
      ></div>
    </div>

    <!-- Hero Section -->
    <div
      class="h-screen flex flex-col justify-center items-center text-center relative z-10"
    >
      <h1
        class="text-6xl md:text-7xl font-extrabold transition-transform duration-500"
        :style="{ transform: `translateY(${scrollY}px)` }"
      >
        Untuk {{ currentCallName }} 💜
      </h1>
      <p class="mt-4 text-lg opacity-80 text-slate-700">
        Selamat Hari Valentine....
      </p>

      <button
        @click="handleSecretClick"
        class="mt-8 bg-purple-500 hover:bg-purple-400 text-white font-bold py-2 px-4 rounded-lg shadow-lg transition transform hover:scale-110 sparkle"
      >
        Klik Aku 💖
      </button>
      <!-- Button Ganti Panggilan -->
      <div class="text-center mt-2 z-20">
        <button
          @click="changeCallName"
          class="bg-purple-500 text-white py-2 px-4 rounded-lg shadow-lg hover:bg-purple-400 transition"
        >
          Ganti Panggilan
        </button>
      </div>
    </div>

    <!-- Quotes Section -->
    <div class="py-16 px-4 md:px-20 bg-transparent bg-opacity-10 z-10 relative">
      <h2 class="text-4xl font-bold text-center mb-8">Kata-Kata Romantis</h2>
      <div class="space-y-8">
        <div
          v-for="(quote, index) in quotes"
          :key="index"
          class="p-6 bg-purple-800 bg-opacity-20 rounded-lg shadow-lg text-lg italic hover:bg-opacity-40 transition sparkle"
        >
          "{{ quote }}"
        </div>
      </div>
    </div>

    <!-- Love Letter Section -->
    <div
      class="py-16 px-4 md:px-20 flex flex-col items-center bg-purple-500 bg-opacity-40 relative z-10"
    >
      <h2 class="text-4xl font-bold text-center mb-6">
        Surat Cinta Untukmu ✉️
      </h2>
      <div
        v-if="!isLetterOpened"
        @click="openLetter"
        class="cursor-pointer p-10 bg-pink-500 rounded-xl shadow-lg hover:bg-pink-400 transition transform hover:scale-105 animate-pulse"
      >
        <p class="text-2xl text-center">Klik untuk Membuka Surat 💌</p>
      </div>
      <div
        v-else
        class="p-8 bg-white text-purple-800 rounded-xl shadow-lg text-center leading-relaxed relative"
      >
        <p v-if="letterSlide === 0">{{ regretMessages[0] }}</p>
        <p v-if="letterSlide === 1">{{ regretMessages[1] }}</p>
        <p v-if="letterSlide === 2">{{ regretMessages[2] }}</p>
        <p v-if="letterSlide === 3">{{ regretMessages[3] }}</p>
        <p v-if="letterSlide === 4">{{ regretMessages[4] }}</p>
        <p v-if="letterSlide === 5">{{ regretMessages[5] }}</p>
        <p v-if="letterSlide === 6">{{ regretMessages[6] }}</p>
        <p v-if="letterSlide === 7">{{ regretMessages[7] }}</p>

        <!-- Navigasi Slide -->
        <div class="mt-4 flex justify-between">
          <button
            @click="prevSlide"
            :disabled="letterSlide === 0"
            class="bg-purple-500 text-white py-2 px-4 rounded-lg hover:bg-purple-400 transition disabled:opacity-50"
          >
            Sebelumnya
          </button>
          <button
            @click="nextSlide"
            :disabled="letterSlide === 7"
            class="bg-purple-500 text-white py-2 px-4 rounded-lg hover:bg-purple-400 transition disabled:opacity-50"
          >
            Selanjutnya
          </button>
        </div>
      </div>
    </div>

    <!-- Final Surprise Message -->
    <div
      v-if="showFinalMessage"
      class="py-16 px-4 md:px-20 bg-transparent text-center text-white z-10"
    >
      <h2 class="text-5xl font-extrabold mb-4 animate-bounce">
        💖 Aku Selalu Menunggumu 💖
      </h2>
      <p class="text-xl opacity-90">
        Tidak peduli berapa lama waktu berlalu, hatiku tetap untukmu.
      </p>
    </div>

    <!-- Secret Message -->
    <div
      v-if="showSecretMessage"
      class="fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center z-50"
    >
      <div
        class="bg-white text-purple-800 p-8 rounded-xl shadow-2xl text-center"
      >
        <h2 class="text-4xl font-bold mb-4">Rahasia Kecil 😍</h2>
        <p class="text-lg">
          Setiap klikmu membuatku semakin yakin, bahwa aku ingin terus
          memperjuangkanmu.
        </p>
        <button
          @click="showSecretMessage = false"
          class="mt-6 bg-purple-500 text-white py-2 px-4 rounded-lg shadow-lg hover:bg-purple-400 transition"
        >
          Tutup 💕
        </button>
      </div>
    </div>

    <!-- Footer -->
    <div class="py-8 text-center text-sm bg-purple-800 z-10 relative">
      <p>Terlepas dari segalanya, aku hanya ingin melihatmu bahagia 💜</p>
    </div>
  </div>
</template>

<style scoped>
/* Animasi Balon/Hati Melayang */
@keyframes float {
  from {
    transform: translateY(100vh) rotate(0deg);
    opacity: 1;
  }
  to {
    transform: translateY(-100px) rotate(360deg);
    opacity: 0;
  }
}

.animate-float {
  animation-name: float;
  animation-timing-function: linear;
  position: absolute;
  animation-iteration-count: infinite; /* Balon tidak berhenti */
  animation-duration: 10s;
}

/* Gradient Bergerak */
.bg-gradient-animation {
  background: linear-gradient(270deg, #ff6ec7, #d76ef5, #f3a3d9);
  background-size: 400% 400%;
  animation: gradientAnimation 15s ease infinite;
}

@keyframes gradientAnimation {
  0% {
    background-position: 0% 50%;
  }
  50% {
    background-position: 100% 50%;
  }
  100% {
    background-position: 0% 50%;
  }
}

.sparkle {
  text-shadow: 0 0 5px rgba(255, 255, 255, 0.5),
    0 0 10px rgba(255, 255, 255, 0.7), 0 0 15px rgba(255, 255, 255, 1);
}
</style>

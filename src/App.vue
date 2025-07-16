<script setup lang="ts">
import { onMounted, ref, computed } from 'vue';
import image1 from './assets/1.png';
import image2 from './assets/2.gif';
import image3 from './assets/3.png';
import image4 from './assets/4.png';

const selectedImage = ref<string | null>(null);
const displayedText = ref('');
const isTyping = ref(false);
const currentLanguage = ref('pt');

type Language = 'pt' | 'en';

type Texts = {
  [key in Language]: {
    greeting: string;
    introduction: string;
    currently: string;
    techStacks: string;
    workTitle: string;
    footerContact: string;
    footerBuilt: string;
    activities: string[];
  };
};

const texts: Texts = {
  pt: {
    greeting: 'Oi!',
    introduction: 'Eu sou <strong>João,</strong> um <strong>Desenvolvedor Fullstack.</strong> Apaixonado por construir soluções simples, mas eficazes.<br /> Estou <strong>sempre</strong> procurando por novas experiências.',
    currently: 'Atualmente',
    techStacks: 'Minhas stacks incluem:',
    workTitle: 'Aqui você pode ver alguns dos meus trabalhos. (Principalmente Gamedev 😁)',
    footerContact: 'Sinta-se à vontade para entrar em contato comigo se quiser!',
    footerBuilt: 'Este site foi construído do zero, usando Vue.JS e Typescript :)',
    activities: ['Programando', 'Jogando', 'Curtindo a vida', 'Malhando', 'Ouvindo música', 'Relaxando']
  },
  en: {
    greeting: 'Hi!',
    introduction: 'I\'m <strong>João,</strong> a <strong>Fullstack Developer.</strong> Passionate about building simple, yet effective solutions.<br /> I\'m <strong>always</strong> looking for new experiences.',
    currently: 'Currently',
    techStacks: 'My tech stacks include:',
    workTitle: 'Here you can see some of my work. (Mostly Gamedev 😁)',
    footerContact: 'Feel free to contact me if you want to!',
    footerBuilt: 'This site was built from scratch, using Vue.JS and Typescript :)',
    activities: ['Coding', 'Playing', 'Enjoying life', 'Pushing Weights', 'Listening music', 'Vibin']
  }
};

const currentTexts = computed(() => texts[currentLanguage.value as Language]);

function toggleLanguage() {
  currentLanguage.value = currentLanguage.value === 'pt' ? 'en' : 'pt';
  whatIamDoing();
}

function openImageModal(image: string) {
  selectedImage.value = image;
}

function closeImageModal() {
  selectedImage.value = null;
}

function showStacks() {
  const stacks = ['Node.JS', 'Go', 'C#', 'React', 'Vue', 'SQLite', 'PostgreSQL', 'Docker'];
  return stacks.map((stack) => `<div class="badge badge-neutral m-1">${stack}</div>`).join('');
}

async function typeText(text: string) {
  if (isTyping.value) return;
  
  isTyping.value = true;
  displayedText.value = '';
  
  for (let i = 0; i <= text.length; i++) {
    displayedText.value = text.slice(0, i);
    await new Promise(resolve => setTimeout(resolve, 100));
  }
  
  isTyping.value = false;
}

let activityInterval: number;

async function whatIamDoing() {
  const options = currentTexts.value.activities;
  
  const getNextActivity = () => {
    const availableOptions = options.filter(option => option !== displayedText.value);
    return availableOptions[Math.floor(Math.random() * availableOptions.length)];
  };
  
  if (activityInterval) {
    clearInterval(activityInterval);
  }
  
  await typeText(options[0]);
  
  activityInterval = setInterval(async () => {
    if (!isTyping.value) {
      const nextActivity = getNextActivity();
      await typeText(nextActivity);
    }
  }, 6000);
}

onMounted(() => {
  whatIamDoing();
});
</script>

<template>
  <div class="language-toggle">
    <button @click="toggleLanguage" class="flag-button" :title="currentLanguage === 'pt' ? 'Switch to English' : 'Mudar para Português'">
      <div class="flag-container">
        <svg v-if="currentLanguage === 'pt'" class="flag-svg" viewBox="0 0 640 480" xmlns="http://www.w3.org/2000/svg">
          <g fill-rule="evenodd" stroke-width="1pt">
            <rect width="640" height="480" fill="#229e45"/>
            <path d="M321.4 436L47.6 244.9L321.4 53.7L595.1 244.9L321.4 436z" fill="#f8e509"/>
            <circle cx="321.4" cy="244.8" r="72" fill="#2b49a3"/>
            <path d="M273.8 207.7c-17.6 0-31.9 14.3-31.9 31.9s14.3 31.9 31.9 31.9 31.9-14.3 31.9-31.9-14.3-31.9-31.9-31.9z" fill="#ffffef"/>
            <path d="M272.7 209.3l-.8 1.7c-5.6 11.9-5.6 25.1 0 37l.8 1.7c6.1-1.2 11.8-3.4 17-6.5l1.4-1.1c.8-8.8.8-17.7 0-26.5l-1.4-1.1c-5.2-3.1-10.9-5.3-17-6.5z" fill="#6b9bd2"/>
            <path d="M285.2 216.8c2.2 0 4.1-1.8 4.1-4.1s-1.8-4.1-4.1-4.1-4.1 1.8-4.1 4.1 1.8 4.1 4.1 4.1z" fill="#ffffef"/>
            <path d="M296.4 232.4c2.2 0 4.1-1.8 4.1-4.1s-1.8-4.1-4.1-4.1-4.1 1.8-4.1 4.1 1.8 4.1 4.1 4.1z" fill="#ffffef"/>
            <path d="M302.6 251.2c2.2 0 4.1-1.8 4.1-4.1s-1.8-4.1-4.1-4.1-4.1 1.8-4.1 4.1 1.8 4.1 4.1 4.1z" fill="#ffffef"/>
            <path d="M296.4 269.9c2.2 0 4.1-1.8 4.1-4.1s-1.8-4.1-4.1-4.1-4.1 1.8-4.1 4.1 1.8 4.1 4.1 4.1z" fill="#ffffef"/>
            <path d="M285.2 285.5c2.2 0 4.1-1.8 4.1-4.1s-1.8-4.1-4.1-4.1-4.1 1.8-4.1 4.1 1.8 4.1 4.1 4.1z" fill="#ffffef"/>
          </g>
        </svg>
        
        <svg v-else class="flag-svg" viewBox="0 0 640 480" xmlns="http://www.w3.org/2000/svg">
          <g fill-rule="evenodd">
            <g stroke-width="1pt">
              <path fill="#bd3d44" d="M0 0h640v480H0z"/>
              <path stroke="#fff" d="M0 55.3h640M0 129.4h640M0 203.5h640M0 277.6h640M0 351.7h640M0 425.8h640M0 499.9h640"/>
              <path fill="#fff" d="M0 18.4h640M0 92.5h640M0 166.6h640M0 240.7h640M0 314.8h640M0 388.9h640M0 463h640"/>
            </g>
            <path fill="#192f5d" d="M0 0h364.8v258.5H0z"/>
            <g fill="#fff">
              <g id="d">
                <g id="c">
                  <g id="e">
                    <g id="b">
                      <path id="a" d="M60.8 15.2l.9 2.8h2.9l-2.4 1.7.9 2.8-2.4-1.7-2.4 1.7.9-2.8-2.4-1.7h2.9z"/>
                      <use transform="translate(60.8 0)" href="#a"/>
                      <use transform="translate(121.6 0)" href="#a"/>
                      <use transform="translate(182.4 0)" href="#a"/>
                      <use transform="translate(243.2 0)" href="#a"/>
                      <use transform="translate(304 0)" href="#a"/>
                    </g>
                    <use transform="translate(0 36.4)" href="#b"/>
                  </g>
                  <use transform="translate(0 72.8)" href="#e"/>
                </g>
                <use transform="translate(0 145.6)" href="#c"/>
              </g>
              <use transform="translate(0 291.2)" href="#d"/>
              <use transform="translate(30.4 18.2)" href="#c"/>
              <use transform="translate(30.4 109.2)" href="#c"/>
              <use transform="translate(30.4 200.2)" href="#c"/>
            </g>
          </g>
        </svg>
      </div>
    </button>
  </div>

  <div class="flex flex-container justify-center m-10">
    <div class="card card-side shadow-xl mb-10">
      <figure>
        <img
          src="https://media.licdn.com/dms/image/v2/D4D03AQGGdCGm1RIqVw/profile-displayphoto-shrink_800_800/profile-displayphoto-shrink_800_800/0/1723066784021?e=1733961600&v=beta&t=zMkbflPCZqhT7QLEx3_bmhWNGsYay127xj8-3RJ-xag"
          alt="Movie" class="card-img"
          @click="openImageModal('https://media.licdn.com/dms/image/v2/D4D03AQGGdCGm1RIqVw/profile-displayphoto-shrink_800_800/profile-displayphoto-shrink_800_800/0/1723066784021?e=1733961600&v=beta&t=zMkbflPCZqhT7QLEx3_bmhWNGsYay127xj8-3RJ-xag')" />
      </figure>
      <div class="card-body">
        <h2 class="card-title">{{ currentTexts.greeting }}</h2>
        <p v-html="currentTexts.introduction"></p>
        <p>
          {{ currentTexts.currently }}
          <span class="typing-text">
            {{ displayedText }}
          </span>
          <span class="dots"></span>
        </p>

        <p>{{ currentTexts.techStacks }} </p>

        <div v-html="showStacks()"></div>
      </div>
    </div>

    <div class="divider"></div>

    <h1>{{ currentTexts.workTitle }}</h1>
    <div class="carousel w-full max-w-lg mx-auto">
      <div id="slide1" class="carousel-item relative w-full">
        <img :src="image1" class="carousel-img" @click="openImageModal(image1)" />
        <div class="absolute left-5 right-5 top-1/2 flex -translate-y-1/2 transform justify-between">
          <a href="#slide4" class="btn btn-circle">❮</a>
          <a href="#slide2" class="btn btn-circle">❯</a>
        </div>
      </div>
      <div id="slide2" class="carousel-item relative w-full">
        <img :src="image2" class="carousel-img" @click="openImageModal(image2)" />
        <div class="absolute left-5 right-5 top-1/2 flex -translate-y-1/2 transform justify-between">
          <a href="#slide1" class="btn btn-circle">❮</a>
          <a href="#slide3" class="btn btn-circle">❯</a>
        </div>
      </div>
      <div id="slide3" class="carousel-item relative w-full">
        <img :src="image3" class="carousel-img" @click="openImageModal(image3)" />
        <div class="absolute left-5 right-5 top-1/2 flex -translate-y-1/2 transform justify-between">
          <a href="#slide2" class="btn btn-circle">❮</a>
          <a href="#slide4" class="btn btn-circle">❯</a>
        </div>
      </div>
      <div id="slide4" class="carousel-item relative w-full">
        <img :src="image4" class="carousel-img" @click="openImageModal(image4)" />
        <div class="absolute left-5 right-5 top-1/2 flex -translate-y-1/2 transform justify-between">
          <a href="#slide3" class="btn btn-circle">❮</a>
          <a href="#slide1" class="btn btn-circle">❯</a>
        </div>
      </div>
    </div>

    <!-- Modal para a imagem -->
    <div v-if="selectedImage" class="modal-overlay" @click="closeImageModal">
      <div class="modal-content">
        <img :src="selectedImage" class="modal-img" />
        <span class="close-button" @click="closeImageModal">✖</span>
      </div>
    </div>
  </div>

  <footer class="footer footer-center bg-base-200 text-base-content rounded p-10">
    <nav>
      <div class="grid grid-flow-col gap-4">
        <a href="https://github.com/oaorotti">
          <svg xmlns="https://github.com/oaorotti" width="24" height="24" fill="currentColor" class="bi bi-github"
            viewBox="0 0 16 16">
            <path
              d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27s1.36.09 2 .27c1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.01 8.01 0 0 0 16 8c0-4.42-3.58-8-8-8" />
          </svg>
        </a>
        <a href="https://www.linkedin.com/in/jo%C3%A3o-wittor-d-882861245/">
          <svg xmlns="https://www.linkedin.com/in/jo%C3%A3o-wittor-d-882861245/" width="24" height="24"
            fill="currentColor" class="bi bi-linkedin" viewBox="0 0 16 16">
            <path
              d="M0 1.146C0 .513.526 0 1.175 0h13.65C15.474 0 16 .513 16 1.146v13.708c0 .633-.526 1.146-1.175 1.146H1.175C.526 16 0 15.487 0 14.854zm4.943 12.248V6.169H2.542v7.225zm-1.2-8.212c.837 0 1.358-.554 1.358-1.248-.015-.709-.52-1.248-1.342-1.248S2.4 3.226 2.4 3.934c0 .694.521 1.248 1.327 1.248zm4.908 8.212V9.359c0-.216.016-.432.08-.586.173-.431.568-.878 1.232-.878.869 0 1.216.662 1.216 1.634v3.865h2.401V9.25c0-2.22-1.184-3.252-2.764-3.252-1.274 0-1.845.7-2.165 1.193v.025h-.016l.016-.025V6.169h-2.4c.03.678 0 7.225 0 7.225z" />
          </svg>
        </a>
        <a
          href="https://mail.google.com/mail/u/0/#inbox?compose=GTvVlcSGLdlnHmgsXscsWXfNddNFlmRVfgngskStbfqLCsXlVxQdsmpSgndwKhqvqmmmPzVqLKvKm">
          <svg
            xmlns="https://mail.google.com/mail/u/0/#inbox?compose=GTvVlcSGLdlnHmgsXscsWXfNddNFlmRVfgngskStbfqLCsXlVxQdsmpSgndwKhqvqmmmPzVqLKvKm"
            width="24" height="24" fill="currentColor" class="bi bi-envelope" viewBox="0 0 16 16">
            <path
              d="M0 4a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v8a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2zm2-1a1 1 0 0 0-1 1v.217l7 4.2 7-4.2V4a1 1 0 0 0-1-1zm13 2.383-4.708 2.825L15 11.105zm-.034 6.876-5.64-3.471L8 9.583l-1.326-.795-5.64 3.47A1 1 0 0 0 2 13h12a1 1 0 0 0 .966-.741M1 11.105l4.708-2.897L1 5.383z" />
          </svg>
        </a>
      </div>
    </nav>
    <aside>
      <p>{{ currentTexts.footerContact }}</p>
      <p>{{ currentTexts.footerBuilt }}</p>
    </aside>
  </footer>
</template>

<style scoped>
.language-toggle {
  position: fixed;
  top: 20px;
  right: 20px;
  z-index: 999;
}

.flag-button {
  background: none;
  border: 2px solid #ddd;
  border-radius: 8px;
  padding: 8px;
  cursor: pointer;
  transition: all 0.3s ease;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  background-color: white;
}

.flag-button:hover {
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  border-color: #007bff;
}

.flag-container {
  display: flex;
  align-items: center;
  justify-content: center;
}

.flag-svg {
  width: 32px;
  height: 24px;
  border-radius: 4px;
  transition: transform 0.3s ease;
}

.flag-button:hover .flag-svg {
  transform: scale(1.05);
}

.flex-container {
  align-items: center;
  flex-direction: column;
  gap: 20px;
}

.card-img {
  max-width: 200px;
  height: auto;
  object-fit: cover;
  cursor: pointer;
}

.carousel {
  max-width: 600px;
}

.carousel-img {
  max-height: 300px;
  width: auto;
  margin: 0 auto;
  object-fit: cover;
  cursor: pointer;
}

.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1000;
}

.modal-content {
  position: relative;
  max-width: 90%;
  max-height: 90%;
}

.modal-img {
  width: 100%;
  height: auto;
}

.close-button {
  position: absolute;
  top: 10px;
  right: 10px;
  color: white;
  font-size: 24px;
  cursor: pointer;
}

.dots::after {
  content: '';
  display: inline-block;
  width: 1ch;
  animation: dots 1.2s steps(4, end) infinite;
}

@keyframes dots {
  0% {
    content: '';
  }

  25% {
    content: '.';
  }

  50% {
    content: '..';
  }

  75% {
    content: '...';
  }

  100% {
    content: '';
  }
}

.typing-text {
  display: inline-block;
  font-family: monospace;
  border-right: 2px solid white;
  animation: blink 0.8s step-end infinite;
  min-width: 1ch;
}

@keyframes blink {
  50% {
    border-color: transparent;
  }
}
</style>
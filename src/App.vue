<script setup lang="ts">
import { ref } from 'vue';
import image1 from './assets/1.png';
import image2 from './assets/2.gif';
import image3 from './assets/3.png';
import image4 from './assets/4.png';

const selectedImage = ref<string | null>(null);

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
</script>

<template>
  <div class="flex flex-container justify-center m-10">
    <div class="card card-side shadow-xl mb-10">
      <figure>
        <img
          src="https://media.licdn.com/dms/image/v2/D4D03AQGGdCGm1RIqVw/profile-displayphoto-shrink_800_800/profile-displayphoto-shrink_800_800/0/1723066784021?e=1733961600&v=beta&t=zMkbflPCZqhT7QLEx3_bmhWNGsYay127xj8-3RJ-xag"
          alt="Movie" class="card-img"
          @click="openImageModal('https://media.licdn.com/dms/image/v2/D4D03AQGGdCGm1RIqVw/profile-displayphoto-shrink_800_800/profile-displayphoto-shrink_800_800/0/1723066784021?e=1733961600&v=beta&t=zMkbflPCZqhT7QLEx3_bmhWNGsYay127xj8-3RJ-xag')" />
      </figure>
      <div class="card-body">
        <h2 class="card-title">Hi!</h2>
        <p>I'm <strong>João,</strong> a <strong>Fullstack Developer.</strong> Passionate about building simple, yet
          effective solutions.
          <br /> I'm <strong>always</strong> looking for new experiences.
        </p>
        <p>Currently, i'm leading a <strong>company</strong> with some friends, while also working as a
          <strong>Freelancer</strong>
        </p>
        <p>My tech stacks include: </p>

        <div v-html="showStacks()"></div>
      </div>
    </div>

    <div class="divider"></div>

    <h1>Here you can see some of my work. (Mostly Gamedev 😁)</h1>
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
        <a href="https://mail.google.com/mail/u/0/#inbox?compose=GTvVlcSGLdlnHmgsXscsWXfNddNFlmRVfgngskStbfqLCsXlVxQdsmpSgndwKhqvqmmmPzVqLKvKm">
          <svg xmlns="https://mail.google.com/mail/u/0/#inbox?compose=GTvVlcSGLdlnHmgsXscsWXfNddNFlmRVfgngskStbfqLCsXlVxQdsmpSgndwKhqvqmmmPzVqLKvKm" width="24" height="24" fill="currentColor" class="bi bi-envelope"
            viewBox="0 0 16 16">
            <path
              d="M0 4a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v8a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2zm2-1a1 1 0 0 0-1 1v.217l7 4.2 7-4.2V4a1 1 0 0 0-1-1zm13 2.383-4.708 2.825L15 11.105zm-.034 6.876-5.64-3.471L8 9.583l-1.326-.795-5.64 3.47A1 1 0 0 0 2 13h12a1 1 0 0 0 .966-.741M1 11.105l4.708-2.897L1 5.383z" />
          </svg>
        </a>
      </div>
    </nav>
    <aside>
      <p>Feel free to contact me if you want to!</p>
      <p>This site was built from scratch, using Vue.JS and Typescript :)</p>
    </aside>
  </footer>
</template>

<style scoped>
.flex-container {
  align-items: center;
  flex-direction: column;
  gap: 20px;
}

.card-img {
  max-width: 200px;
  /* Ajusta o tamanho da imagem do card */
  height: auto;
  object-fit: cover;
  cursor: pointer;
  /* Indica que a imagem é clicável */
}

.carousel {
  max-width: 600px;
  /* Limita a largura total do carrossel */
}

.carousel-img {
  max-height: 300px;
  /* Limita a altura das imagens no carrossel */
  width: auto;
  /* Mantém a proporção da largura */
  margin: 0 auto;
  /* Centraliza a imagem no carrossel */
  object-fit: cover;
  /* Ajusta a imagem para caber na altura sem distorcer */
  cursor: pointer;
  /* Indica que a imagem é clicável */
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
</style>

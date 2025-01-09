<template>
  <section id="about">
      <!-- <h3>Sobre mí</h3>
      <div class="positionRelative">
          <div>
              <div class="about_group">
                  <p class="big_green_number">01</p>
                  <span class="title_afterNumber">Quién soy?</span>
                  <p class="about_text">Highly adaptable Web Developer with a passion for learning new technologies. I have experience in a range of programming languages including HTML, CSS, JavaScript, PHP, React and Vue. In addition to those skills, I'm well-versed in Git, GitHub and MySQL.</p>
              </div>
              <div class="about_group">
                  <p class="big_green_number">02</p>
                  <span class="title_afterNumber">Cuáles son mis skills?</span>
                  <p class="about_text">Maquetado front-end con <span class="accent">HTML</span> y <span class="accent">CSS</span> Programación web con <span class="accent">JavaScript</span>, <span class="accent">PHP</span>, <span class="accent">React</span> y <span class="accent">Vue</span>
                      Manejo y mantención de bases de datos con <span class="accent">MySQL</span> y <span class="accent">PostgreSQL</span>
                      + Prototipado con <span class="accent">Figma</span>
                      + <span class="accent">Inglés</span> profesional</p>
              </div>
              <div class="about_group">
                  <p class="big_green_number">03</p>
                  <span class="title_afterNumber">Cuál es mi experiencia laboral?</span>
                  <div v-for="(experience, index) in experiences" :key="index" class="about_text">
                      <p class="about_text_company">{{experience.company}} ({{calculateTotalWorked(experience)}})</p>
                      <p class="itemTitle">{{experience.jobTitle}}</p>
                      <p class="about_text_time">{{experience.fromTime.slice(7,16)}} - {{experience.toTime.slice(7,16)}}</p>
                      <ul v-for="(tarea, index) in experience.tareas" :key="index">
                          <li>{{ tarea }}</li>
                      </ul>
                  </div>
              </div>
          </div>
          <div id="ctn_aboutPhrase">
              <p id="about_phrase">Para saber más ingresá acá</p>
              <div>
                  <a href="" target="_blank">CV</a>
                  <a href="https://github.com/MartinaFSA" target="_blank">GitHub</a>
                  <a href="https://www.linkedin.com/in/martina-fernandez-suarez-anzorena/" target="_blank">LinkedIn</a>
              </div>
          </div>
          <div id="about_ctnFigures">
              <img class="star" id="about_star" src="/src/assets/img/star.svg" alt="">
              <div class="halfCircle" id="about_halfCircle"></div>
              <div class="fullCircle" id="about_firstFullCircle"></div>
              <div class="fullCircle" id="about_sndFullCircle"></div>
          </div>
      </div> -->
  </section>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>

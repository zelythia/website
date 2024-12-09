<script>
import FooterDiv from "./components/FooterDiv.vue";
import NavigationBar from "./components/NavigationBar.vue";
import ProjectCategoryTile from "./components/ProjectCategoryTile.vue";
import ProjectDescription from "./components/ProjectDescription.vue";
import ProjectTile from "./components/ProjectTile.vue";

export default {
  components: {
    NavigationBar,
    ProjectCategoryTile,
    ProjectTile,
    ProjectDescription,
    FooterDiv,
  },

  data() {
    return {
      visibleDescription: "start",
    };
  },

  methods: {
    changeProject(project) {
      project = project.toLowerCase();
      if (project == "") return;
      if (this.visibleDescription == project) {
        this.visibleDescription = "start";
        return;
      }
      this.visibleDescription = project;
    },
  },

  mounted() {
    const allowedLocations = ["start", "autotools", "ae", "archify", "tio", "pong"];
    const hash = window.location.hash.substring(1);

    if (hash == "") return;

    document.getElementById("projects").scrollIntoView();
    if (allowedLocations.includes(hash)) {
      this.visibleDescription = hash;
      return;
    }
    window.location.hash = "projects";
  },
};
</script>

<template>
  <header><NavigationBar></NavigationBar></header>

  <main>
    <div id="aboutMe" class="sectionContainer">
      <img src="/media/icon_large+drawing.png" alt="Big zelythia/lukaz logo with references to my projects" class="homeImage" />

      <div class="homeContent">
        <span href="" class="sectionTitle">About me</span>
        <h1>zelythia/lukaz</h1>

        <div class="homeContentText">
          <h2>- Lukas Z.</h2>
          <h2>- Student/Developer</h2>
          <h2>- 19 y/o</h2>
          <h2>- Germany</h2>
        </div>

        <div class="homeButtonContainer noselect">
          <a href="https://github.com/zelythia" target="_blank" rel="noreferrer noopener" class="button imageButton">
            <img alt="image" src="/media/github-icon.png" class="buttonImage" />
          </a>

          <a href="https://twitter.com/zelythia" target="_blank" rel="noreferrer noopener" class="button imageButton">
            <img alt="image" src="/media/twitter-icon.png" class="buttonImage" />
          </a>

          <a href="https://ko-fi.com/zelythia" target="_blank" rel="noreferrer noopener" class="button imageButton">
            <img alt="image" src="/media/kofi_symbol.svg" class="buttonImage" />
          </a>
        </div>
      </div>
    </div>

    <div class="sectionContainer" id="projects">
      <div class="projectsDiv noselect">
        <!-- Minecraft -->
        <ProjectCategoryTile
          imageSrc="https://imgs.search.brave.com/ZHP3_JaTXX7R1mc1QaZVggyLbGGUOW1tkwoTbVApJN0/rs:fit:1000:1000:1/g:ce/aHR0cHM6Ly9neWF6/by5jb20vYTRhYmM1/ZmRiOTY1ZDFiOTdk/YjM4NDUzMDEyZWZj/NzMvdGh1bWIvMTAw/MA"
        >
          <div class="innerProjectContainer">
            <ProjectTile
              imageSrc="/media/AutoToolsLogo.png"
              @click="changeProject('AutoTools')"
              :highlighted="visibleDescription == 'AutoTools'"
            ></ProjectTile>

            <ProjectTile imageSrc="/media/AE.png" @click="changeProject('')" :highlighted="visibleDescription == 'AE'">
            </ProjectTile>
          </div>
        </ProjectCategoryTile>

        <!-- Discord -->
        <ProjectCategoryTile
          imageSrc="https://assets-global.website-files.com/6257adef93867e50d84d30e2/636e0a69f118df70ad7828d4_icon_clyde_blurple_RGB.svg"
        >
          <div class="innerProjectContainer">
            <ProjectTile
              imageSrc="/media/archify/archify_green.png"
              @click="changeProject('Archify')"
              :highlighted="visibleDescription == 'Archify'"
            ></ProjectTile>
          </div>
        </ProjectCategoryTile>

        <!-- Games -->
        <ProjectCategoryTile imageSrc="/media/game-controller.svg">
          <div class="innerProjectContainer">
            <ProjectTile
              imageSrc="/media/games/TIO/icon.png"
              @click="changeProject('TIO')"
              :highlighted="visibleDescription == 'TIO'"
            ></ProjectTile>
            <ProjectTile
              imageSrc="/media/games/pong/icon.ico"
              @click="changeProject('pong')"
              :highlighted="visibleDescription == 'pong'"
            ></ProjectTile>
          </div>
        </ProjectCategoryTile>
      </div>

      <!-- Default Description -->
      <ProjectDescription title="Projects" v-if="visibleDescription == 'start'">
        <p>
          This is a collection of all my public available projects. Most of them also have their source code availabel at
          <a href="https://github.com/zelythia" target="_blank" class="link">Github</a>.
        </p>

        <div>
          <a
            href="https://github.com/zelythia/JungleJumper"
            target="_blank"
            rel="noreferrer noopener"
            class="button imageButton labeledButton"
          >
            <img alt="image" src="/media/github-icon.png" class="buttonImage" />

            <a href=""><b>Jungle Jumper</b></a>
          </a>
        </div>
      </ProjectDescription>

      <!-- Minecraft -->
      <ProjectDescription title="AutoTools" v-if="visibleDescription == 'autotools'">
        <div>
          <video autoplay muted loop style="width: 100%; border-radius: 10px">
            <source src="/media/autotools/AutoTools.mp4" />
          </video>

          <div class="minecraftDiv_1">
            <p style="margin-top: 0">
              AutoTools is a Minecraft mod that allows you to automatically switch to the best tool for blocks/mobs with the press
              of a button. It looks through your whole inventory and choses the best tool according to mining level/speed, damage,
              enchantments.
            </p>

            <a href="https://www.curseforge.com/minecraft/mc-mods/autotools" target="_blank">
              <img
                style="width: 150px; height: 150px; border-radius: 10px; margin-left: 10px"
                src="/media/autotools/curseforge-icon.jpg"
                alt="Download at Curseforge"
                class="highlight_hover"
              />
            </a>
          </div>
        </div>
      </ProjectDescription>

      <ProjectDescription title="" v-if="visibleDescription == 'ae'">
        <p style="font-size: 300px; text-align: center; margin: 0">AE</p>
      </ProjectDescription>

      <!-- Discord -->
      <ProjectDescription title="Archify" v-if="visibleDescription == 'archify'">
        <p style="margin-top: 0">
          Archify is a simple Discord-Bot that lets you save messages from servers, just by right clicking the message. The Bot
          uses Discord.js to communicate with the Discord-API and it's entire source code is available at Github.
        </p>

        <div class="discordDiv_1">
          <img
            src="/media/archify/save.png"
            alt="Save by right clicking a message"
            style="border-radius: 10px; min-height: 170px; width: 100%"
          />

          <div style="display: flex; gap: 10px; flex-direction: column; justify-content: center">
            <a
              href="https://github.com/zelythia/discord-archify"
              target="_blank"
              rel="noreferrer noopener"
              class="button imageButton"
            >
              <img alt="image" src="/media/github-icon.png" class="buttonImage" />
            </a>

            <a
              href="https://discord.com/oauth2/authorize?client_id=936276333309337622&scope=bot%20applications.commands&permissions=1024"
              class="button"
              style="background-color: rgb(79, 84, 92)"
              target="_blank"
              >Invite</a
            >
          </div>
        </div>
      </ProjectDescription>

      <!-- Games -->
      <ProjectDescription title="Trash It out!" v-if="visibleDescription == 'tio'">
        <div class="tioDesc_1" style="display: flex; gap: 20px">
          <img class="tioImg_1" src="/media/games/TIO/image.jpg" alt="" />

          <div style="display: flex; flex-direction: column">
            <p style="margin-top: 0">
              Trash it out! is a mobile game made with the Unity GameEngine. The main objective of the game is to sort the trash
              falling from the sky into the corresponding bins. <br />
              <br />
              It is currently only available on the Amazon Appstore or as a direkt download on this page.
            </p>

            <div class="tioDesc_2">
              <a href="/download/TrashItOut!.apk" download target="_blank" rel="noreferrer noopener" class="button imageButton">
                <img alt="image" src="/media/download-icon.svg" class="buttonImage" />
              </a>

              <a href="">
                <img
                  class="link standaloneButtonImage"
                  src="/media/games/TIO/amazon-appstore-icon.png"
                  alt=""
                  style="border-radius: 10px"
                />
              </a>
            </div>
          </div>
        </div>
      </ProjectDescription>

      <ProjectDescription title="Pong" v-if="visibleDescription == 'pong'">
        <img src="/media/games/pong/pong.png" alt="Pong Game" style="width: 100%; border-radius: 10px" />

        <p>
          This is a simple Pong Game made with the Godot Game Engine. It features a 1 Player-Mode against the AI and a 2
          Players-Mode against each other. There still is potential for updates like different difficulties and maybe a
          multiplayer mode, that may come in the future.<br />
          Right now it's available to play on <a href="https://zelythia.itch.io/pong" target="_blank" class="link">itch.io</a> and
          there are also downloads available for Windows and Linux.
        </p>

        <div style="display: flex; flex-direction: row; gap: 25px">
          <img src="/media/games/pong/itch.io.svg" alt="Itch.io" style="height: 70px" />

          <a
            href="/download/Pong.zip"
            target="_blank"
            rel="noreferrer noopener"
            class="button imageButton"
            style="height: 55px; width: 55px"
            download
          >
            <img alt="image" src="/media/download-icon.svg" class="buttonImage" style="height: 50px" />
          </a>
        </div>
      </ProjectDescription>
    </div>
  </main>

  <footer>
    <FooterDiv></FooterDiv>
  </footer>
</template>

<style scoped>
footer {
  min-height: 50px;
  background-color: var(--background-darker);
  display: flex;
  align-items: center;
}

header {
  position: fixed;
  width: 100%;
  top: 0;
  display: flex;
  z-index: 100;
  align-items: center;
  justify-content: center;
}

#aboutMe {
  align-items: center;
  flex-direction: row;
  justify-content: center;
}

#projects {
  flex-direction: row;
  margin: 0 80px;
  align-items: flex-start;
  height: 90vh;
}

.projectsDiv {
  display: flex;
  flex-direction: row;
  gap: 20px;
  flex-wrap: wrap;
  margin-top: 120px;
  justify-content: center;
  min-width: 200px;
  max-width: 200px;
  max-height: 60vh;
  overflow: scroll;
  scrollbar-width: none; /* Firefox */
  -ms-overflow-style: none; /* IE and Edge*/
  padding: 0 10px 60px;
  z-index: 100;
}

.projectsDiv::-webkit-scrollbar {
  display: none;
}

.projects {
  display: flex;
  flex-direction: row;
  gap: 20px;
  margin-left: -20px;
}

.homeContent {
  height: auto;
  display: flex;
  align-self: center;
  align-items: stretch;
  flex-direction: column;
}

.homeContent h1 {
  margin: 0;
}

.homeContent h2 {
  margin: 6px;
}

.homeImage {
  width: 400px;
  height: 600px;
  object-fit: cover;
  border-radius: 5px;
  margin-right: 30px;
}

.buttonImage {
  max-width: 60px;
  height: auto;
  align-self: center;
  object-fit: cover;
}

.homeButtonContainer {
  flex: 0 0 auto;
  width: 100%;
  display: flex;
  margin-top: 16px;
  align-items: center;
  margin-left: 8px;
  flex-direction: row;
  justify-content: flex-start;
  gap: 48px;
}

.imageButton {
  width: 70px;
  height: 70px;
  display: flex;
  align-items: center;
  flex-direction: row;
  justify-content: center;
  text-decoration: none;
  padding: 8px;

  cursor: pointer;
  font-style: normal;
  transition: 0.3s;
  border-radius: 4px;
  background-color: var(--button-bg);
}

.standaloneButtonImage {
  width: 86px;
  height: 86px;
  border-radius: 10px;
}

.minecraftDiv_1 {
  display: flex;
  flex-direction: row;
}

.discordDiv_1 {
  display: flex;
  justify-content: center;
  margin-bottom: 30px;
  gap: 20px;
}

.tioImg_1 {
  width: 50%;
  border-radius: 10px;
}

.tioDesc_2 {
  display: flex;
  gap: 20px;
}

.labeledButton {
  flex-direction: column;
  padding-top: 20px;
  padding-bottom: 20px;
  width: max-content !important;
}

.labeledButton a {
  color: var(--background);
  margin-top: 10px;
}

.labeledButton:hover a {
  text-decoration: underline;
}

@media (max-width: 1100px) {
  .discordDiv_1 {
    flex-direction: column;
    align-items: center;
  }

  .discordDiv_1 .imageButton {
    width: 140px;
    height: 140px;
  }

  .discordDiv_1 .buttonImage {
    width: 110px;
    height: 110px;
  }
}

@media (max-width: 950px) {
  .tioDesc_1 {
    flex-direction: column-reverse;
  }

  .tioImg_1 {
    width: 100%;
  }

  .tioDesc_2 {
    justify-content: center;
  }
}

@media (max-width: 820px) {
  h1 {
    font-size: 10vw;
  }

  h2 {
    font-size: 5vw;
  }

  #aboutMe {
    flex-direction: column-reverse;
    height: 200%;
  }

  .homeContent {
    padding-top: 250px;
    height: 100vh;
    align-items: center;
  }

  .homeContent h2 {
    margin: 1vw;
  }

  .homeContentText {
    display: flex;
    flex-direction: column;
  }

  .homeButtonContainer {
    justify-content: center;
    gap: 10vw;
    margin-left: 0;
  }

  .imageButton {
    width: 95px;
    height: 95px;
  }

  .buttonImage {
    width: 15vw;
  }

  .standaloneButtonImage {
    width: 111px;
    height: 111px;
    border-radius: 10px;
  }

  .sectionTitle {
    font-size: 3vw;
    margin-left: 2vw;
  }

  .homeImage {
    width: 90vw;
    height: auto;
    margin: 0;
  }

  #projects {
    flex-direction: column;
    margin: 0;
    height: auto;
  }

  .projectsDiv {
    min-width: auto;
    max-width: 100%;
    width: 92vw;
    padding: 0 4vw;

    flex-direction: row;
    flex-wrap: nowrap;

    overflow-x: auto;
    height: 100%;
    padding-top: 20px;
    min-width: -moz-fit-content;
    justify-content: flex-start;
  }

  .innerProjectContainer {
    border-radius: 20px;
    padding: 0;
    margin: 0;
    width: auto;
    padding: 10px;
    flex-wrap: nowrap;
    height: fit-content;
  }

  .projectDescription {
    margin: 100px 2vw 2vw;
    height: max-content;
  }

  .minecraftDiv_1 {
    flex-direction: column !important;
    align-items: center;
    gap: 20px;
  }
}

@media (min-width: 1100px) {
  h1 {
    font-size: 3rem;
  }

  h2 {
    font-size: 1.5rem;
  }

  .sectionTitle {
    font-size: 1rem;
  }

  .imageButton {
    width: 100px;
    height: 100px;
  }

  .homeButtonContainer {
    gap: 32px;
  }

  .buttonImage {
    max-width: 90px;
    height: auto;
  }

  .standaloneButtonImage {
    width: 116px;
    height: 116px;
  }

  .homeImage {
    margin-right: 50px;
    height: 60vh;
    width: auto;
  }

  p {
    font-size: 1.25rem;
  }
}
</style>

<template>
  <div class="navbar">
    <img src="/media/logo.png" alt="Zelythia" class="logo" />

    <div class="nav">
      <!-- Links -->

      <div class="navLinks">
        <a href="#aboutMe" class="navLink">Home</a>
        <a href="#projects" class="navLink">Projects</a>
        <!-- <a href="#blog" class="navLink">Blog</a> -->
      </div>

      <a href="https://github.com/zelythia" class="button" target="_blank">Github</a>

      <a href="https://github.com/zelythia" class="button kofi" style="margin-left: 20px" target="_blank">
        <img src="https://storage.ko-fi.com/cdn/brandasset/v2/kofi_symbol.png" alt="" style="vertical-align: sub; height: 20px" />
        Support me on Ko-fi
      </a>

      <!-- ModeToggle -->
      <div class="slider noselect" ref="modeToggle" @click="toggleMode()">
        <img src="" alt="Icon" class="toggleIcon" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    toggleMode() {
      this.$refs.modeToggle.classList.toggle("on");
      this.$refs.modeToggle.childNodes[0].classList.toggle("on");

      //Dark Mode
      if (this.$refs.modeToggle.classList.contains("on")) {
        document.documentElement.style.setProperty("--accent-color", "#329181ff");

        document.documentElement.style.setProperty("--background", "#181818");
        document.documentElement.style.setProperty("--background-darker", "#111111");
        document.documentElement.style.setProperty("--background-lighter", "#222222");
        document.documentElement.style.setProperty("--background-highlighted", "#272727");
        document.documentElement.style.setProperty("--projects-background", "#353e44");

        document.documentElement.style.setProperty("--text", "#ccc");
        document.documentElement.style.setProperty("--text-alt", "#ccc");

        document.documentElement.style.setProperty("--button-bg", "#ccc");
        document.documentElement.style.setProperty("--button-hover-bg", "rgb(29, 29, 29)");

        document.documentElement.style.setProperty("--logo-bg", "#ccc");
        return;
      }

      //Light Mode
      document.documentElement.style.setProperty("--accent-color", "#329181ff");

      document.documentElement.style.setProperty("--background", "#ffffff");
      document.documentElement.style.setProperty("--background-darker", "#eeeeee");
      document.documentElement.style.setProperty("--background-lighter", "#e2eef9");
      document.documentElement.style.setProperty("--background-highlighted", "#f9f4f0ff");
      document.documentElement.style.setProperty("--projects-background", "#f9f4f0ff");

      document.documentElement.style.setProperty("--text", "#191919");
      document.documentElement.style.setProperty("--text-alt", "#0f1722ff");

      document.documentElement.style.setProperty("--button-bg", "rgba(0, 0, 0, 0.1)");
      document.documentElement.style.setProperty("--button-hover-bg", "rgba(145, 67, 50, 0.1)");

      document.documentElement.style.setProperty("--logo-bg", "rgba(0,0,0,0)");
    },
  },
  mounted() {
    if (window.matchMedia && window.matchMedia("(prefers-color-scheme: dark)").matches) {
      this.$refs.modeToggle.classList.toggle("on");
      this.$refs.modeToggle.childNodes[0].classList.toggle("on");
    }

    window.matchMedia("(prefers-color-scheme: dark)").addEventListener("change", (event) => {
      if (!event.matches) return;
      this.$refs.modeToggle.classList.toggle("on");
      this.$refs.modeToggle.childNodes[0].classList.toggle("on");
    });
  },
};
</script>

<style>
.navbar {
  margin: 15px;
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 24px 10px 24px;
  max-width: 80vw;
  background-color: var(--background-darker);
  border-radius: 10px;
}

@media (max-width: 1500px) {
  .navbar {
    max-width: 100vw;
  }
}

@media (max-width: 1300px) {
  .navbar {
    max-width: 90vw;
  }
}

.logo {
  height: 40px;
  background-color: var(--logo-bg);
  border: 20px;
  border-radius: 5px;
  padding: 0 5px;
}

.nav {
  flex: 0 0 auto;
  display: flex;
  align-items: center;
  flex-direction: row;
}

.navLinks {
  margin-right: 48px;
  flex: 0 0 auto;
  display: flex;
  align-items: center;
  flex-direction: row;
}

.navLink {
  font-size: 16px;
  font-family: DM Sans;
  font-weight: 500;
  line-height: 1.6;
  letter-spacing: 0.02em;
  text-transform: capitalize;
  text-decoration: none;
  cursor: pointer;
  transition: 0.3s;
  margin-left: 41px;
  color: vaR(--text);
}

.slider {
  position: relative;
  width: 70px;
  height: 40px;
  cursor: pointer;
  -webkit-transition: 0.4s;
  transition: 0.4s;
  border-radius: 5px;
  margin-left: 20px;
  background-color: var(--background-lighter);
}

.slider:hover {
  background-color: var(--accent-color);
}

.slider.on:hover {
  box-shadow: 0 0 5px 2px rgba(255, 255, 255, 0.7);
  background-color: var(--background-lighter);
}

.toggleIcon {
  height: 24px;
  width: 24px;
  position: absolute;
  left: 6px;
  bottom: 8px;
  transition: 0.4s;
  -webkit-transition: 0.4s;
  content: url("/media/sun.png");
}

.toggleIcon.on {
  -webkit-transform: translateX(26px);
  -ms-transform: translateX(26px);
  transform: translateX(32px);
  content: url("/media/moon.png");
}

@media (min-width: 1100px) {
  .navLink {
    font-size: 18px;
  }

  .button {
    font-size: 18px !important;
  }
}
</style>

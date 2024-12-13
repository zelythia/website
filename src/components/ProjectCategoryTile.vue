<script>
export default {
  data() {
    return {
      visible: false,
    };
  },
  name: "ProjectCategoryTile",
  props: {
    imageSrc: String,
  },
  methods: {},
};
</script>

<template>
  <div class="projectCategoryTile" @click="visible = !visible">
    <img :src="imageSrc" alt="" class="projectImage" />
  </div>

  <Transition>
    <slot v-if="visible"></slot>
  </Transition>
</template>

<style>
.innerProjectContainer {
  width: 160px;
  margin-top: -40px;
  display: flex;
  flex-wrap: wrap;
  row-gap: 10px;
  align-content: center;
  padding-top: 40px;
  background-color: var(--projects-background);
  padding-bottom: 10px;
  border-radius: 0 0 20px 20px;
  margin-bottom: -10px;
  flex-direction: column;
}

.v-enter-active {
  transition: all 0.2s ease-out;
}
.v-leave-active {
  transition: all 0.2s ease-out;
}

.v-enter-from,
.v-leave-to {
  transform: translateY(-200px);
  opacity: 0;
}

.projectCategoryTile {
  min-width: 160px;
  height: 160px;

  border-radius: 20px;
  background-color: var(--background-lighter);

  display: flex;
  justify-content: center;
  align-items: center;

  transition: transform 0.1s;
  cursor: pointer;
  z-index: 10;
}

.projectCategoryTile:hover {
  transform: scale(1.025);
  box-shadow: 0 0 3px #666666;
  filter: brightness(1.1);
}

.projectImage {
  max-width: 70%;
  max-height: 70%;
  min-width: 50%;
  border-radius: 5px;
}

.projectContainer {
  display: none;
}
</style>

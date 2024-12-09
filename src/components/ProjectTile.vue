<script>
export default {
  name: "ProjectTile",
  props: {
    imageSrc: String,
    highlighted: {
      type: Boolean,
      default: false,
      required: true,
    },
  },
};
</script>

<template>
  <div class="projectTile" :class="highlighted ? 'highlighted' : ''">
    <img :src="imageSrc" alt="" class="projectImage" />
  </div>
</template>

<style>
.projectTile {
  width: 140px;
  min-height: 140px;
  margin: 0px 0;

  border-radius: 20px;
  background-color: var(--background-lighter);

  display: flex;
  justify-content: center;
  align-items: center;

  transition: transform 0.1s;
  cursor: pointer;
}

.highlighted {
  transform: scale(1.02);
  box-shadow: 0 0 3px #666666;
  filter: brightness(1.1);
  background-color: var(--background-highlighted);
}

.projectTile:hover {
  transform: scale(1.02);
  box-shadow: 0 0 3px #666666;
  filter: brightness(1.1);
}
</style>

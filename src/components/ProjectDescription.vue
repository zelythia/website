<script>
export default {
  name: "ProjectDescription",
  props: {
    title: {
      type: String,
      default: "Project Title",
    },
  },
};
</script>

<template>
  <div class="projectDescription">
    <h1>{{ title }}</h1>

    <slot></slot>
  </div>
</template>

<style>
.projectDescription {
  background-color: var(--background-lighter);
  border-radius: 10px;
  height: 60vh;
  max-width: 700px;
  z-index: 20;
  transition: transform 0.1s padding 0.1s;
  cursor: default;
  margin-top: 120px;
  font-size: 20px;
  padding: 20px 20px 40px;
  flex-grow: 1;
  overflow: scroll;
  scrollbar-width: none; /* Firefox */
  -ms-overflow-style: none; /* IE and Edge*/
}

.projectDescription::-webkit-scrollbar {
  display: none;
}

.projectDescription:hover {
  box-shadow: 0 0 3px #666666;
}

.projectDescription h1 {
  margin: -20px 0 0;
  margin-bottom: 0;
}
</style>

<script></script>

<template>
  <div class="footer">
    <p class="left-section">2025</p>
    <a href="mailto:dev@zelythia.net" clas="center-section navlink">dev@zelythia.net</a>
    <p>©lukas/zelythia</p>
  </div>
</template>

<style>
.footer p {
  margin: 0 20px;
}

.footer {
  display: flex;
  width: 100%;
  justify-content: space-between;
  align-items: center;
  margin: 0 50px;
}

.left-section {
  text-align: left;
}

.right-section {
  text-align: right;
}

.center-section {
  text-align: center;
  flex: 1; /* This will make the center section take up all remaining space between the left and right sections */
}
</style>

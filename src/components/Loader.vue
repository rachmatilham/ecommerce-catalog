<template>
  <div class="overlay">
    <div class="loader"></div>
  </div>
</template>

<script></script>

<style>
.overlay {
  width: 100vw;
  height: 100vh;
  position: absolute;
  background-color: gray;
  opacity: 0.7;
  z-index: 99;
}
.loader {
  border: 16px solid #f3f3f3; /* Light grey */
  border-top: 16px solid #3498db; /* Blue */
  border-radius: 50%;
  width: 120px;
  height: 120px;
  animation: spin 2s linear infinite;
  position: absolute;
  top: 45%;
  left: 45%;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>

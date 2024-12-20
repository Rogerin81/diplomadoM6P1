<template>
  <div id="app" class="container">
    <img src="@/assets/logousip.png" alt="Logo" class="logo" />
    <h1>Diplomado FullStack</h1>
    <h3>Sexta Versión</h3>
    <p class="creator">Creado por: <strong>Roger Armando Ibarra Chavarría</strong></p>
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  font-family: Arial, sans-serif;
}

.logo {
  object-fit: cover;
  margin-bottom: 20px;
}

h1 {
  font-size: 36px;
  color: #333;
}
.creator {
  font-size: 18px;
  color: #555;
  margin-top: 20px;
  text-align: center;
}

.creator strong {
  color: #000;
}
</style>
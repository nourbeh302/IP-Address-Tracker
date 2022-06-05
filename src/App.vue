<template>
  <section class="App">
    <div class="container">
      <h2>IP Address Tracker</h2>
      <div class="input-field">
        <input type="text" placeholder="Enter an IP Address or press ENTER" />
        <span class="icon">
          <img src="./assets/arrow-right.svg" alt="" srcset="" />
        </span>
      </div>
      <!-- Card component goes here -->
    </div>
    <div id="map"></div>
  </section>
</template>

<script>
export default {
  name: "App",
  components: {}
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@100;200;300;400;500;600;700;800;900&display=swap");

:root {
  --clr-white: hsl(180, 0%, 95%);
  --clr-black: hsl(180, 0%, 10%);
  --clr-grey: hsl(180, 0%, 35%);
  --ff-text: "Inter", sans-serif;
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: var(--ff-text);
}

.App {
  height: 100vh;
  display: grid;
  grid-template-rows: 4fr 9fr;
}

.container {
  gap: 1em;
  background: url("./assets/pattern-bg.png") no-repeat center center;
  background-size: cover;
  padding: 2em;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.container > h2 {
  color: var(--clr-white);
}

.input-field {
  display: flex;
  width: 50%;
  max-width: 400px;
}

.input-field > input {
  height: 100%;
  padding: 1em;
  width: 100%;

  outline: none;
  border-radius: 8px 0px 0px 8px;
  border: none;
  text-overflow: ellipsis;
}

.input-field > span.icon {
  border-radius: 0px 8px 8px 0px;
  padding: 14px;
  height: 44px;
  background: var(--clr-black);
}

img {
  width: auto;
  height: 100%;
  object-fit: cover;
}

@media all and (max-width: 767px) {
  .input-field {
    width: 100%;
  }
}
</style>

<template>
  <div class="IPCard">
    <div id="address">
      <small>IP Address</small>
      <h3>{{ IPInfo.address }}</h3>
    </div>
    <div id="state">
      <small>Location</small>
      <h3>{{ IPInfo.state }}</h3>
    </div>
    <div id="timezone">
      <small>Timezone</small>
      <h3>{{ IPInfo.timezone }}</h3>
    </div>
    <div id="isp">
      <small>ISP</small>
      <h3>{{ IPInfo.isp }}</h3>
    </div>
  </div>
</template>

<script>
export default {
  name: "IPCard",
  props: ["IPInfo"],
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.IPCard {
  background: var(--clr-white);
  box-shadow: 0px 0px 16px var(--shadow);
  border-radius: 0.25rem;

  z-index: 4;
  position: absolute;
  top: 11em;
  display: flex;
  flex-wrap: wrap;
  gap: 2em 3em;
  padding: 2em 5em;
}

.IPCard h3 {
  font-weight: normal;
  color: var(--clr-primary);
}

small {
  text-transform: uppercase;
  letter-spacing: 2px;
  color: var(--clr-black);
}

@media all and (max-width: 725px) {
  .IPCard {
    width: 60%;
    gap: 0.75em;
    top: 10em;
    padding: 2em;
  }
}
</style>

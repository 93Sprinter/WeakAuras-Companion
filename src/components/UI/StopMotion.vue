<template>
  <div id="StopMotion">
    <div>
      <div class="title">{{ $t('app.stopmotion.selectgifconverter' /* StopMotion GIF Converter */) }}</div>
      <br/>
      <div class="bts-top-right">
        <Button class="btn-ok btn-title" v-if="step == 3" @click="setStep(1)">
        <span class="material-icons">first_page</span>
        </Button>
        <Button class="btn-ok btn-title" v-if="step > 1" @click="prev()">
        <span class="material-icons">keyboard_backspace</span>
        </Button>
      </div>
    </div>
    <StopMotionSelectGif v-if="step == 1" @next="next()"/>
    <StopMotionSettings v-if="step == 2" :wowVersions="wowVersions" @next="next()"/>
    <StopMotionResult v-if="step == 3"/>
  </div>
</template>

<script>
import StopMotionSelectGif from "./StopMotionSelectGif.vue"
import StopMotionSettings from "./StopMotionSettings.vue";
import StopMotionResult from "./StopMotionResult.vue"
import Button from "./Button.vue";
//import { useStopMotionStore } from "@/stores/stopmotion";

export default {
  name: "StopMotion",
  components: {
    StopMotionSelectGif,
    StopMotionSettings,
    StopMotionResult,
    Button
  },
  props: ["wowVersions"],
  data() {
    return {
      step: 1,
    };
  },
  methods: {
    setStep(value) {
      this.step = value
    },
    next() {
      this.step++;
    },
    prev() {
      this.step--;
    },
  }
};
</script>

<style scoped lang="scss">
#StopMotion {
  padding: 5px 0 5px 2.35vw;
  text-align: left;
  overflow: auto;
  height: 100%;
  width: 100%;
}

.config-row {
  display: flex;
  flex-wrap: wrap;
}

.config-row-item {
  flex: 50%;
}

label,
.label {
  color: #eeeeee;
  margin: 10px 0 5px;
  font-size: 14px;
}

.title {
  margin: 20px 0 10px;
}

.block {
  margin-left: 15px;
  font-size: 15px;
}

@font-face {
  font-family: pass;
  font-style: normal;
  font-weight: 400;
  src: url("data:application/font-woff;charset=utf-8;base64,d09GRgABAAAAAATsAA8AAAAAB2QAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAABGRlRNAAABWAAAABwAAAAcg9+z70dERUYAAAF0AAAAHAAAAB4AJwANT1MvMgAAAZAAAAA/AAAAYH7AkBhjbWFwAAAB0AAAAFkAAAFqZowMx2N2dCAAAAIsAAAABAAAAAQAIgKIZ2FzcAAAAjAAAAAIAAAACAAAABBnbHlmAAACOAAAALkAAAE0MwNYJ2hlYWQAAAL0AAAAMAAAADYPA2KgaGhlYQAAAyQAAAAeAAAAJAU+ATJobXR4AAADRAAAABwAAAAcCPoA6mxvY2EAAANgAAAAEAAAABAA5gFMbWF4cAAAA3AAAAAaAAAAIAAKAE9uYW1lAAADjAAAARYAAAIgB4hZ03Bvc3QAAASkAAAAPgAAAE5Ojr8ld2ViZgAABOQAAAAGAAAABuK7WtIAAAABAAAAANXulPUAAAAA1viLwQAAAADW+JM4eNpjYGRgYOABYjEgZmJgBEI2IGYB8xgAA+AANXjaY2BifMg4gYGVgYVBAwOeYEAFjMgcp8yiFAYHBl7VP8wx/94wpDDHMIoo2DP8B8kx2TLHACkFBkYA8/IL3QB42mNgYGBmgGAZBkYGEEgB8hjBfBYGDyDNx8DBwMTABmTxMigoKKmeV/3z/z9YJTKf8f/X/4/vP7pldosLag4SYATqhgkyMgEJJnQFECcMOGChndEAfOwRuAAAAAAiAogAAQAB//8AD3jaY2BiUGJgYDRiWsXAzMDOoLeRkUHfZhM7C8Nbo41srHdsNjEzAZkMG5lBwqwg4U3sbIx/bDYxgsSNBRUF1Y0FlZUYBd6dOcO06m+YElMa0DiGJIZUxjuM9xjkGRhU2djZlJXU1UDQ1MTcDASNjcTFQFBUBGjYEkkVMJCU4gcCKRTeHCk+fn4+KSllsJiUJEhMUgrMUQbZk8bgz/iA8SRR9qzAY087FjEYD2QPDDAzMFgyAwC39TCRAAAAeNpjYGRgYADid/fqneL5bb4yyLMwgMC1H90HIfRkCxDN+IBpFZDiYGAC8QBbSwuceNpjYGRgYI7594aBgcmOAQgYHzAwMqACdgBbWQN0AAABdgAiAAAAAAAAAAABFAAAAj4AYgI+AGYB9AAAAAAAKgAqACoAKgBeAJIAmnjaY2BkYGBgZ1BgYGIAAUYGBNADEQAFQQBaAAB42o2PwUrDQBCGvzVV9GAQDx485exBY1CU3PQgVgIFI9prlVqDwcZNC/oSPoKP4HNUfQLfxYN/NytCe5GwO9/88+/MBAh5I8C0VoAtnYYNa8oaXpAn9RxIP/XcIqLreZENnjwvyfPieVVdXj2H7DHxPJH/2/M7sVn3/MGyOfb8SWjOGv4K2DRdctpkmtqhos+D6ISh4kiUUXDj1Fr3Bc/Oc0vPqec6A8aUyu1cdTaPZvyXyqz6Fm5axC7bxHOv/r/dnbSRXCk7+mpVrOqVtFqdp3NKxaHUgeod9cm40rtrzfrt2OyQa8fppCO9tk7d1x0rpiQcuDuRkjjtkHt16ctbuf/radZY52/PnEcphXpZOcofiEZNcQAAeNpjYGIAg///GBgZsAF2BgZGJkZmBmaGdkYWRla29JzKggxD9tK8TAMDAxc2D0MLU2NjENfI1M0ZACUXCrsAAAABWtLiugAA")
    format("woff");
}

#sync {
  text-align: center;
  width: 100%;
  margin: auto;
  transition: all 0.4s ease-in-out;
}

#sync.top {
  position: relative;
  top: 10px;
}

.btn-issue span,
.btn-refresh span {
  position: relative;
  bottom: 8px;
  line-height: 50px;
  cursor: pointer;
}

.btn-title {
  height: 40px;
}
.material-icons {
  font-size: 34px;
  vertical-align: top;
  cursor: pointer;
}

.btn-refresh.spin {
  background: #ababab;
  border-color: transparent;
  color: #313131;
}

.btn-issue,
.btn-refresh {
  padding: 12px 15px;
  padding-left: 13px;
}

.explorer {
  cursor: pointer;
  font-size: 12px;
  margin-top: 5px;
  color: rgb(255, 209, 0);
  font-weight: 500;
}

.center {
  position: relative;
  left: 50%;
  transform: translate(-50%, 0);
  margin: 20px 0 0;
  max-width: 100%;
}

.bts-top-right{
  position: absolute;
  right: 40px;
  top: 30px;
}

</style>

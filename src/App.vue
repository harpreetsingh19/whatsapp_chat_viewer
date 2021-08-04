<template>
  <div id="app">
    <b-modal
      v-if="!viewContent"
      ref="verify"
      @ok="submit"
      :ok-disabled="popupOk"
      ok-only
      @hidden="closePopup"
      title="Give password"
      :no-close-on-backdrop="true"
      :no-close-on-esc="true"
      data-backdrop="static"
      centered
    >
      <label for="p">Password</label>&nbsp;
      <input type="password" v-model="pass"  @mouseleave="validate"/>
    </b-modal>
    <reader v-if="viewContent"></reader>
  </div>
</template>

<script>
import reader from "@/components/reader.vue";
export default {
  name: "App",
  components: { reader },
  data() {
    return {
      pass: "",
      viewContent: false,
      popupOk: true,
    };
  },
  methods: {
    validate() {
      if (this.pass == "admin") {
        this.popupOk = false;
      }
      else{
        this.popupOk=true
      }
    },
    submit() {
      if (this.pass == "admin") {
        this.viewContent = true;
      }
    },
    closePopup() {
      this.$refs.verify.hide();
    },
  },
  mounted() {
    this.$refs.verify.show();
  },
};
</script>

<style>
#app {
  font-family: sans-serif, Avenir, Helvetica, Arial;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin: 0;
  padding: 0;
}
.close {display: none;}
</style>

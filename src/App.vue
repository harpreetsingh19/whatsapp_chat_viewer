<template>
  <div id="app">
    <!-- <b-modal
      v-if="!viewContent"
      ref="verify"
      @ok="submit"
      :ok-disabled="popupOk"
      ok-only
      @hidden="closePopup"
      title="Give password"
      :no-close-on-backdrop="true"
      :no-close-on-esc="true"
      centered
    >
    <svg xmlns="http://www.w3.org/2000/svg" width="50" height="50" fill="currentColor" class="bi bi-file-lock2-fill" viewBox="0 0 16 16">
  <path d="M7 6a1 1 0 0 1 2 0v1H7V6z"/>
  <path d="M12 0H4a2 2 0 0 0-2 2v12a2 2 0 0 0 2 2h8a2 2 0 0 0 2-2V2a2 2 0 0 0-2-2zm-2 6v1.076c.54.166 1 .597 1 1.224v2.4c0 .816-.781 1.3-1.5 1.3h-3c-.719 0-1.5-.484-1.5-1.3V8.3c0-.627.46-1.058 1-1.224V6a2 2 0 1 1 4 0z"/>
</svg>
&nbsp;
      <input placeholder="Type admin" type="password" v-model="pass"  @mouseleave="validate"/>
    </b-modal> -->
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
      viewContent: true,
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
      //this.$refs.verify.hide();
    },
  },
  mounted() {
    //this.$refs.verify.show();
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

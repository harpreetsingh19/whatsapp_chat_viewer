<template>
  <div>
    <b-modal
      ref="inputBox"
      @ok="submit"
      :ok-disabled="popupOk"
      @hidden="closePopup"
      title="Give Input"
      :no-close-on-backdrop="true"
      :no-close-on-esc="true"
      centered
    >
      <input type="file" ref="doc" id="doc" @change="fileValue" /> <br />
      <div v-if="warningMsg !== ''" class="warn">{{ warningMsg }}</div>
      <br />
      <b-dropdown
        id="dropdown-dropright"
        dropright
        text="Your Name"
        variant="primary"
        class="m-2"
        :disabled="warning || senderAvailabe"
      >
        <b-dropdown-item
          :value="firstPerson"
          :text="firstPerson"
          @click="person = firstPerson"
          >{{ firstPerson }}</b-dropdown-item
        >
        <b-dropdown-item
          :value="secondPerson"
          :text="secondPerson"
          @click="person = secondPerson"
          >{{ secondPerson }}</b-dropdown-item
        >
      </b-dropdown>
    </b-modal>
  </div>
</template>

<script>
export default {
  name: "InputPopup",
  props: {
    firstPerson: String,
    secondPerson: String,
    senderAvailabe: Boolean,
  },
  data() {
    return {
      person: "",
      warningMsg: "",
      warning: false,
    };
  },
  methods: {
    fileValue() {
      if (this.$refs.doc.files[0].type == "text/plain") {
        this.$emit("input-file", this.$refs.doc.files[0]);
        this.warningMsg = "";
        this.warning = false;
      } else {
        this.warningMsg = "Please Select text file";
        this.warning = true;
      }
    },
    submit() {
      this.$emit("input-file", this.$refs.doc.files[0]);
      this.$emit("name", this.person);
      this.closePopup();
    },
    closePopup() {
      this.$emit("close", false);
      this.$refs.inputBox.hide();
    },
  },
  mounted() {
    this.$refs.inputBox.show();
  },
  computed: {
    popupOk() {
      return this.person != "" ? false : true;
    },
  },
};
</script>
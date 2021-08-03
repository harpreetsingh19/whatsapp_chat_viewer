<template>
  <div>
    <b-modal
      ref="inputBox"
      @ok="submit"
      @hidden="closePopup"
      title="Give Input"
      :no-close-on-backdrop="true"
      :no-close-on-esc="true"
      centered
    >
      <input type="file" ref="doc" id="doc" @change="fileValue" />
      <b-dropdown
        id="dropdown-dropright"
        dropright
        text="Your Name"
        variant="primary"
        class="m-2"
        :disabled="senderAvailabe"
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
    };
  },
  methods: {
    fileValue() {
      this.$emit("input-file", this.$refs.doc.files[0]);
    },
    submit() {
      this.$emit("input-file", this.$refs.doc.files[0]);
      this.$emit("name", this.person);
      this.closePopup();
    },
    closePopup() {
      this.$emit("close", false);
      this.$refs.inputBox.hile();
    },
  },
  mounted() {
    this.$refs.inputBox.show();
  },
};
</script>
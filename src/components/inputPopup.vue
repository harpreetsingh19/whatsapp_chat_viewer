<template>
  <div>
    <b-modal ref="inputBox" 
    @ok="submit" 
    @hidden="closePopup" 
    title="Give Input"
    centered
    >
      <input type="file" ref="doc" id="doc" />
      <input type="text" v-model="person" />
    </b-modal>
  </div>
</template>

<script>
export default {
  name: "InputPopup",
  data() {
    return {
      person: "",
    };
  },
  methods: {
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
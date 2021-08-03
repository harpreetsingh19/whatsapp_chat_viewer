<template>
  <div>
    <Guide v-if="!ultest"></Guide>
    <b-button
      v-if="!ultest"
      class="start-button"
      @click="openInputPopup"
      variant="outline-success"
      >START</b-button
    >
    <InputPopup
      v-if="openInputBox"
      @input-file="onFileInput"
      @name="ownerName"
      @close="closeInputPopup"
      :firstPerson="personOne"
      :secondPerson="personTwo"
      :senderAvailabe="senderAvail"
    ></InputPopup>

    <!-- <span data-testid="tail-in" data-icon="tail-in" class="_3nrYb"
      ><svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 8 13"
        width="8"
        height="13"
      >
        <path
          opacity=".13"
          fill="#0000000"
          d="M1.533 3.568L8 12.193V1H2.812C1.042 1 .474 2.156 1.533 3.568z"
        ></path>
        <path
          fill="currentColor"
          d="M1.533 2.568L8 11.193V0H2.812C1.042 0 .474 1.156 1.533 2.568z"
        ></path></svg
    ></span>
    <span data-testid="tail-out" data-icon="tail-out" class="_3nrYb"
      ><svg
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 8 13"
        width="8"
        height="13"
      >
        <path
          opacity=".13"
          d="M5.188 1H0v11.193l6.467-8.625C7.526 2.156 6.958 1 5.188 1z"
        ></path>
        <path
          fill="currentColor"
          d="M5.188 0H0v11.193l6.467-8.625C7.526 1.156 6.958 0 5.188 0z"
        ></path></svg
    ></span> -->
    <div v-if="ultest">
      <ul v-for="(item, index) in allMessage" :key="index" id="printing">
        <div v-if="item.msg != 'nan'">
          <li v-if="item.sender == person1.toLowerCase()">
            <div class="owner">
              <div class="mainboxowner">
                <div class="msgbox">
                  {{ item.msg }}
                </div>
                <div class="datetime">
                  <span>{{ item.time }}</span>
                </div>
              </div>
            </div>
          </li>
          <li v-else>
            <div class="partner">
              <div class="mainboxpartner">
                <div class="msgbox">
                  {{ item.msg }}
                </div>
                <div class="datetime">
                  <span>{{ item.time }}</span>
                </div>
              </div>
            </div>
          </li>
        </div>
      </ul>
    </div>
  </div>
</template>

<script>
import InputPopup from "@/components/inputPopup.vue";
import Guide from "@/components/guide.vue";
export default {
  name: "reader",
  components: {
    InputPopup,
    Guide,
  },
  data() {
    return {
      content: [],
      file: "",
      lines: [],
      allMessage: {},
      ultest: false,
      person1: "",
      hideForm: true,
      openInputBox: false,
      personOne: "",
      personTwo: "",
      senderAvail: true,
    };
  },
  methods: {
    openInputPopup() {
      this.openInputBox = true;
    },
    ownerName(e) {
      this.person1 = e;
      this.ultest = true;
    },
    closeInputPopup(e) {
      this.openInputBox = e;
    },
    submitAll() {
      if (this.person1) {
        this.hideForm = false;
      }
    },
    onFileInput(e) {
      this.file = e;
      const reader = new FileReader();
      reader.onload = (res) => {
        this.file = res.target.result;
        this.lines = this.file.split(/\r\n|\n/);
        //   this.content=lines.join('\r\n');
        this.content = this.lines;
        for (let index = 0; index < this.content.length; index++) {
          const element = this.content[index];
          if (element.match(/[0-3][0-9]\/[0-1][0-9]\/\d{2,4},/)) {
            var i = index;
          } else {
            this.content[i] = this.content[i] + " " + element;
          }
        }
        this.messageSender(this.content);
      };
      reader.onerror = (err) => console.log(err);
      reader.readAsText(this.file);
    },
    messageSender(line) {
      for (let index = 0; index < line.length; index++) {
        const message = {
          date: "",
          time: "",
          sender: "",
          msg: "no msg",
        };
        const element = line[index];
        if (element.match(/[0-3][0-9]\/[0-1][0-9]\/\d{2,4},/)) {
          var timeMsg = element.split(" - ");
          var dateTime = timeMsg[0].split(", ");
          if (dateTime[0] && dateTime[1]) {
            message.date = dateTime[0].trim();
            message.time = dateTime[1].trim();
          } else {
            message.date = "nan";
            message.time = "nan";
          }
          var senderMsg = timeMsg[1].split(": ");
          if (senderMsg[0] && senderMsg[1]) {
            message.sender = senderMsg[0].toLowerCase().trim();
            if (this.personOne == "") {
              this.personOne = message.sender;
            }
            if (message.sender != this.personOne) {
              this.personTwo = message.sender;
            }
            message.msg = senderMsg[1].trim();
          } else {
            message.sender = "nan";
            message.msg = "nan";
          }
          this.allMessage[index] = message;
        } else {
          //countelse++;
        }
      }
      if (this.personOne && this.personTwo) {
        this.senderAvail = false;
      }
    },
  },
};
</script>

<style>
</style>
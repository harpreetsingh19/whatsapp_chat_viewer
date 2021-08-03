<template>
  <div>
    <div v-if="hideForm">
      <input type="file" ref="doc" id="doc" @change="onFileInput" />
      <input type="text" v-model="person1" />
      <button @click="submitAll">ok</button>
    </div>

    <!-- <button @click="PrintPanel" v-if="!fileInput">PRINT</button> -->
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
export default {
  name: "reader",
  data() {
    return {
      content: [],
      file: "",
      lines: [],
      allMessage: {},
      ultest: false,
      fileInput: true,
      person1: "",
      hideForm: true,
    };
  },
  methods: {
    submitAll() {
      if (this.person1) {
        this.hideForm = false;
      }
    },
    onFileInput() {
      this.file = this.$refs.doc.files[0];
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
        console.log(this.content);
        this.messageSender(this.content);
      };
      reader.onerror = (err) => console.log(err);
      reader.readAsText(this.file);
    },
    messageSender(line) {
      var countelse = 0;
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
            message.msg = senderMsg[1].trim();
          } else {
            message.sender = "nan";
            message.msg = "nan";
          }
          this.allMessage[index] = message;
        } else {
          countelse++;
          console.log(element);
        }
      }
      this.ultest = true;
      this.fileInput = false;
      console.log(countelse);
    },
  },
};
</script>

<style>
</style>
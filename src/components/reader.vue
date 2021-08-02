<template>
  <div>
    <input type="file" ref="doc" id="doc" @change="onFileInput" />
    <button @click="trigger">trigger</button>
    <span data-testid="tail-in" data-icon="tail-in" class="_3nrYb"
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
    ></span>
    <span v-if="t" style="color: white"> a </span>
    <ul v-for="(item, index) in allMessage" :key="index">
      <div v-if="item.msg != 'no msg'">
        <li v-if="item.sender == person1">
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
      t: false,
      person1: "harpreet",
      person2: "navneet",
    };
  },
  methods: {
    onFileInput() {
      this.file = this.$refs.doc.files[0];
      const reader = new FileReader();
      reader.onload = (res) => {
        this.file = res.target.result;
        this.lines = this.file.split(/\r\n|\n/);
        //   this.content=lines.join('\r\n');
        debugger;
        this.content = this.lines;
        this.messageSender(this.content);
      };
      reader.onerror = (err) => console.log(err);
      reader.readAsText(this.file);
    },
    trigger() {
      this.t = !this.t;
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
        if (element.match(/\d\d\W\d\d/)) {
          message.date = element.substring(0, 8);
          message.time = element.substring(10, 18);
          var nameAndMsg = element.substring(19, line.length).split(":");
          if (nameAndMsg[0].substring(0, 2) == "- ") {
            message.sender = nameAndMsg[0]
              .substring(2, nameAndMsg[0].length)
              .trim()
              .toLowerCase();
          } else {
            message.sender = nameAndMsg[0].trim().toLowerCase();
          }
          if (nameAndMsg[1]) {
            message.msg = nameAndMsg[1];
          } else {
            message.msg = "no msg";
          }
          this.allMessage[index] = message;
        } else {
          console.log("else =>" + element + " =>   " + index);
        }
      }
      console.log(this.allMessage);
    },
  },
};
</script>

<style>
.owner {
  color: rgb(255, 255, 255);
  width: fit-content;
  margin-left: auto;
  margin-right: 3%;
}
.partner {
  color: rgb(124, 124, 209);
  width: fit-content;
  margin-left: 3%;
}
.mainboxowner {
  background-color: coral;
  text-align: right;
  padding: 10px;
  border: none;
  border-radius: 11px;
  border-top-right-radius: 0;
}
.mainboxpartner {
  background-color: darkmagenta;
  text-align: left;
  padding: 10px;
  border: none;
  border-radius: 11px;
  border-top-left-radius: 0;
}
ul {
  padding-inline-start: 0;
}
ul li {
  list-style-type: none;
}
.rigthtail {
  color: black;
}
.datetime {
  text-align: end;
}
</style>
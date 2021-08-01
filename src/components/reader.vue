<template>
  <div>
    <input type="file" ref="doc" id="doc" @change="onFileInput" /> 
    <button @click="trigger">trigger</button>
    <span v-if="t"> a </span>
    <ul v-for="(item,index) in allMessage" :key="index">
      <li>{{item.sender}}</li>
    </ul>
    out 
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
      t:false
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
        this.content = this.lines;
        this.messageSender(this.content);
      };
      reader.onerror = (err) => console.log(err);
      reader.readAsText(this.file);
    },
    trigger(){
      this.t=!this.t;
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
        if (element.match(/[0-9][0-9]/)) {
          message.date = element.substring(0, 8);
          message.time = element.substring(10, 18);
          var nameAndMsg = element.substring(19, line.length).split(":");debugger
          if (nameAndMsg[0].substring(0,2)=="- ") {
          message.sender = nameAndMsg[0].substring(2,nameAndMsg[0].length);
          }
          else{
          message.sender = nameAndMsg[0];
          }
          if(nameAndMsg[1]){

          message.msg = nameAndMsg[1];
          }
          else{
            
          message.msg = "no msg"
          }
          this.allMessage[index] = message;
          //console.log("match =>  " +element.substring(0,8) +" time =>"+element.substring(10,18)+"name" + element.substring(19,line.length));
        } else {
          //line[index-1]+=element;
        }
      }console.log(this.allMessage);
    },
  },
};
</script>

<style>
</style>
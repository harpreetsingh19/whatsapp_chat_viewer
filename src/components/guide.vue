<template>
  <b-container class="guides">
    <span class="heading-content">
      <h3>Guide</h3>
    </span>
    <b-row>
      <b-col>
        <h5>Why</h5>
        <ul>
          <li>When you export your whats-app chat in text format.</li>
          <li>As you can't restore it in your whats-app.</li>
          <li>
            This site helps to view your exported text file as whats-app
            messages.
          </li>
        </ul>
      </b-col>
      <b-col>
        <h5>How</h5>
        <ol>
          <li>Export your chat in text format.</li>
          <li>Click on the above <b>START</b> button.</li>
          <li>Attach your file.</li>
          <li>Choose your name from drop-down in that popup.</li>
        </ol>
      </b-col>
      <!-- <b-col>
          <h5>Print</h5>
          <ul>
              <li>
                  This site will load your message in parts.
              </li>
              <li>There will be a button <strong>NEXT</strong> to go to next page. </li>
              <li>When you want to save your whole chat in <i>PDF</i> format click on <strong>PRINT</strong> button and then "CTRL+P" </li>
          </ul>
      </b-col> -->
    </b-row>
    <p class="note1">
      Note:- Whats-app's limit to export chat as text format in 40,000 messages
    </p>
    <p class="note2">
      So if your text file is having that much message print (Ctrl+P) will take
      its time to load all the pages
    </p>
    <p class="note3">Be Patient</p>
    <br />
    <span class="feedback">Feel free to give</span> &nbsp;
    <a
      href="mailto:singhh.harpreet19@gmail.com?subject = Feedback about whatsapp chat viewer & body = Bug/Problem:-"
      >Feedback</a
    >
  </b-container>
</template>

<script>
export default {
  name: "Guide",
};
</script>

<style>
.feedback {
  color: white;
}
.guides {
  position: absolute;
  top: 300px;
  left: 50%;
  transform: translate(-50%, -50%);
  color: black;
}
i {
  color: rgb(255, 255, 255);
}
a {
  color: green;
}
</style>
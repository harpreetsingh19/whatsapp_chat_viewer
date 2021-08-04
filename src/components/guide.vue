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
      <b-col>
          <h5>Navigation</h5>
          <ul>
              <li>
                  This site will load your message in parts.
              </li>
              <li>There will be <strong>NEXT</strong> & <strong>PREVIOUS</strong> button for navigation. </li>
          </ul>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <h5>Pros</h5>
          <ul>
              <li>
                  This site process every data in your browser.That means we don't save your files in any server.
              </li>
              <li>Your data is SAFE</li>
          </ul>
      </b-col>
      <b-col>
        <h5>Cons</h5>
          <ul>
              <li>
                  As we process every data in browser.Sometimes there will be a lag/delay in response.
              </li>
              <li>But trust me you won't notice it.</li>
          </ul>
      </b-col>
    </b-row>
    <p class="note1">
      Note:- For now this site is not applicable for <em>group chats</em> .
    </p>
    <br />
    <span class="feedback">Feel free to give</span>
    <a
      href="mailto:singhh.harpreet19@gmail.com?subject = Feedback about whatsapp chat viewer & body = Bug/Problem:-"
      > Feedback</a
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
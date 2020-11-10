<template>
  <div class="chat">
    <div id="messages">
      <ul>
        <li v-for="(msg, index) in sortTimes" :key="index">
          <div v-if="msg.id === myId">
            {{ msg.time | dateFormatAll }}{{ msg.message }} me
          </div>
          <div v-else>
            {{ msg.time | dateFormatAll }}{{ msg.message }} other
          </div>
        </li>
      </ul>
    </div>
    <div>
      <input type="text" v-model="inputMessage" />
      <button v-on:click="sendMessage">send</button>
      <label
        ><input
          type="radio"
          v-model="from"
          value="1"
          checked="checked"
        />me</label
      >
      <label><input type="radio" v-model="from" value="2" />other</label>
    </div>
  </div>
</template>

<script>
import moment from "moment";

// for Test
var testDate = new Date();
testDate.setDate(testDate.getDate() - 1);

export default {
  name: "Chat",
  props: {},
  filters: {
    dateFormatAll(date) {
      return moment(date).format("YYYY/MM/DD hh:mm:ss");
    },
    dateFormatTime(date) {
      return moment(date).format("hh:mm:ss");
    },
  },
  data: function () {
    return {
      myId: 1,
      from: 1,
      inputMessage: "",
      messages: [
        {
          id: 1,
          message: "apple",
          time: testDate,
        },
        {
          id: 2,
          message: "orage",
          time: testDate.setMinutes(testDate.getMinutes() + 1),
        },
        {
          id: 3,
          message: "peach",
          time: testDate.setMinutes(testDate.getMinutes() + 1),
        },
        {
          id: 4,
          message: "lemon",
          time: testDate.setMinutes(testDate.getMinutes() + 1),
        },
      ],
    };
  },
  methods: {
    sendMessage: function (event) {
      this.messages.push({
        id: this.from,
        message: this.inputMessage,
        time: new Date(),
      });
      this.inputMessage = "";
    },
  },
  computed: {
    sortTimes: function () {
      return this.messages.sort((a, b) => new Date(a.time) - new Date(b.time));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>

<template>
  <div class="back">
    <div class="header">
      <status-icon :connected="user.connected"/>{{ user.username }}
    </div>

    <ul class="messages" id="scrollall">
      <li
        v-for="(message, index) in user.messages"
        :key="index"
        class="message"
        :class="{ me: message.fromSelf}"
      >
        <div v-if="displaySender(message, index)" 
            class="sender"
            :class="{ me_sender : message.fromSelf}">
          {{ message.fromSelf ? "me" : user.username }}
        </div>
        {{ message.content }}
      </li>
    </ul>

    <form @submit.prevent="onSubmit" class="form">
      <textarea v-model="input" placeholder="Your message..." class="input" />
      <button :disabled="!isValid" class="send-button"><img src="../../../../images/paper-plane.png" style="width: 50%;"/></button>
    </form>
  </div>
</template>

<script>
import StatusIcon from "./StatusIcon";

export default {
  name: "MessagePanel",
  components: {
    StatusIcon,
  },
  props: {
    user: Object,
  },
  data() {
    return {
      input: "",
    };
  },
  methods: {
    onSubmit() {
      this.$emit("input", this.input);
      this.input = "";
      window.scroll({
        top: document.body.scrollHeight,
        left: 0,
        behavior: "smooth"
      });
    },
    displaySender(message, index) {
      return (
        index === 0 ||
        this.user.messages[index - 1].fromSelf !==
          this.user.messages[index].fromSelf
      );
    },
  },
  computed: {
    isValid() {
      return this.input.length > 0;
    },
  },
};

</script>

<style scoped>

*{
font-family: Cambria, Cochin, Georgia, Times, 'Times New Roman', serif;
}

.header {
  position: fixed;
  width:76%;
  margin-left:1%;
  background-color: white;
  line-height: 36px;
  padding: 10px 20px;
  box-shadow: 0px 12px 8px -15px #111;
  font-size: 22px;
  border-radius: 0 0 15px 15px;
}

.back{
  background-color: #d7e6f1;
}
.messages {
  font-size: 16px;
  margin: 0;
  padding-top: 60px;
  padding-right: 20px;
  padding-bottom: 135px;
  padding-left: 20px;
  font-size: 17px;
  display: flex;
  align-items: flex-start;
  flex-direction: column;
  scroll-behavior: smooth;
}

.message {
  list-style: none;
  max-width:45%;
  word-wrap:break-word;
  background-color: #fff;
  box-shadow: 0px 10px 10px rgba(113, 113, 113, 0.1);
  border-radius: 10px;
  padding-top: 0.3rem;
  padding-right: 1rem;
  padding-bottom: 0.4rem;
  padding-left: 1rem;
  margin-top: 10px;
}

.me {
  align-self: flex-end;
  background-color: rgb(240, 251, 255);
}
.me_sender {
  text-align: right;
}
.sender {
  font-weight: bold;
  font-size: 18px;
}

.form {
  width: 76%;
  padding:10px 20px;
  bottom:0;
  margin-left:1%;
  position: fixed;
  display: flex;
  flex-direction: row;
  align-items: center;
  background-color: #fff;
  box-shadow: 0px -12px 8px -15px #111;
  border-radius: 15px 15px 0 0;
}

.input {
  width: 45%;
  resize: none;
  line-height: 1;
  border: none;
  outline: none;

  flex: 1;
  color: rgb(48, 48, 49);
  border: 1px solid #e2e5f1;
  border-radius: 10px;
  font-size: 18px;
  padding: 10px;
  margin-right: 5px;
  cursor: auto;
}

.send-button {
  width: 60px;
  height: 60px;
  background-color: #48abe0;
  color: white;
  border: none;
  padding-top: 5px;
  padding-right: 7px;
  box-shadow: 0 2px 4px darkslategray;
  cursor: pointer;
  transition: all 0.2s ease;
  border-radius: 50%;
}

.send-button:active {
  background-color: #48abe0;
  box-shadow: 0 0 2px darkslategray;
  transform: translateY(2px);
}


textarea::-webkit-scrollbar {
  width: 15px;     
}

textarea::-webkit-scrollbar-thumb {
  background-color: rgb(255, 255, 255);  
  border-radius: 20px;    
  border: 4px solid rgb(192, 187, 179); 
}

</style>


<template>
    <div class="chat-container">
  
      <div v-for="(chat, user) in chats" :key="user" class="chat-window">
        <h2>user {{ user + 1 }}</h2>
          <div class="messages">
            <div v-for="(message, index) in messages" :key="index" :class="{'me': message.user === user, 'anyUser': message.user !== user}" class="message">
              {{ message.content }}
            </div>
          </div>
          <div class="controls">
            <input class="controls__elem" v-model="newMessage[user]" @keyup.enter="sendMessage(user)" placeholder="Поле для ввода сообщения" />
            <input class="controls__elem" type="button" @click="sendMessage(user)" value="Отправить" />
          </div>
      </div>
  
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const chats = [0,1];
  
  const messages = ref([]);
  
  const newMessage = [];
  
  const sendMessage = (user) => {
    if (newMessage[user] == undefined || newMessage[user] == '') return;
    messages.value.push({user: user, content: newMessage[user]});
    newMessage[user] = '';
  };
  
  </script>
  
  <style>
  .chat-container {
    display: flex;
    justify-content: space-around;
    margin: 0 auto;
    max-width: 1000px;
  }
 
  .chat-window {
    width: 45%;
    border: 1px solid #ccc;
    padding: 10px;
  }
  
  .messages {
    display: flex;
    flex-direction: column;
    height: 300px;
    overflow-y: auto;
    border: 1px solid #eee;
    padding: 10px;
    margin-bottom: 10px;
  }
  
  .message {
    margin: 7px;
    padding: 15px;
    width: 60%;
    text-align: center;
  }
  
  .me {
    border: 1px solid #eee;
    align-self: flex-end;
  }
  
  .anyUser {
    border: 1px solid #eee;
  }
  
  .controls {
    display: flex;
  }
  .controls__elem {
    flex-grow: 1;
  }

  ::placeholder {
    text-align: center;
  }
  </style>
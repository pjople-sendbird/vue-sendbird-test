<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";

/**
 * Sendbird
 * You should create a class but for this simple test
 * I will place all here in this file
 */
import Sendbird from "sendbird";

/**
 * This is your Sendbird Application ID (https://dashboard.sendbird.com)
 */
var APP_ID = "D1CB1742-A4A3-44B9-9E7F-126D14BAB34B"; 

/**
 * Any user_id from your account
 */
var USER_ID = "test2"; 

/**
 * Users can have access tokens 
 */
var ACCESS_TOKEN = null;  

/**
 * Any identifier for your handlers 
 * https://sendbird.com/docs/chat/v3/javascript/guides/event-handler
 */
const UNIQUE_HANDLER_ID = "ANY-IDENTIFIER-HERE";  

/**
 * Initialize Sendbird
 */
var sb = new Sendbird({ appId: APP_ID });

/**
 * Connect to Websockets
 */
sb.connect(USER_ID, ACCESS_TOKEN, (user, error) => {
  /**
   * You have a User object
   */
  console.dir(user); console.dir(error);
  /**
   * Create a channel handler to 
   * receive events for messages 
   * and channels
   */
  var channelHandler = new sb.ChannelHandler();
  channelHandler.onMessageReceived = function (channel, message) {
    /**
     * New message arrived
     */
    console.log("onMessageReceived");
    console.dir(message);
  };
  sb.addChannelHandler(UNIQUE_HANDLER_ID, channelHandler);
});

export default {
  name: "Home",
  components: {
    HelloWorld,
  },
};
</script>

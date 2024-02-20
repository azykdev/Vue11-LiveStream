<template>
  <div class="bg-grey-darken-4" style="height: 100vh;">
    <v-row class="ma-0" style="height: 100%;">
      <v-col cols="12" md="9" class="bg-grey-darken-3"
        style="display: flex; flex-direction: column; justify-content: space-between;">

        <div id="video" class="bg-grey w-100 d-flex justify-center align-center pa-5">
          <!-- <video width="300px" ref="videoElement" autoplay></video> -->
          <vue-webrtc ref="webrtc" width="100%" roomId="sample-room">
          </vue-webrtc>
        </div>

        <div id="actions" class="d-flex justify-center pa-2 align-center">
          <v-btn class="mx-2" variant="outlined" :icon="stream ? 'mdi-video' : 'mdi-video-off'"
            @click="videoToggle"></v-btn>
          <v-btn class="mx-2" variant="outlined" :icon="microphone ? 'mdi-microphone' : 'mdi-microphone-off'"
            @click="microphoneToggle"></v-btn>
          <v-btn class="mx-2" variant="outlined" icon="mdi-close" @click="" color="red"></v-btn>
        </div>

      </v-col>
      <v-col cols="12" md="3">
        <v-list lines="two" class="bg-grey-darken-3  rounded">
          <v-list-item class="" v-for="user in users" :key="user.id" :title="user.name"
            prependAvatar="https://cdn-icons-png.freepik.com/512/3177/3177440.png">
          </v-list-item>
        </v-list>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import { VueWebRTC } from 'vue-webrtc';

export default {
  components: {
    'vue-webrtc': VueWebRTC,
  },
  data() {
    return {
      stream: true,
      microphone: true,
      users: [],
      img: null,
    }
  },
  methods: {
    join() {
      this.$refs.webrtc.join()
    },
    leave() {
      this.$refs.webrtc.leave()
    },
    onUserJoined(user) {
      this.users.push(user)
    },
    videoToggle() {
      this.stream = !this.stream
    },
    microphoneToggle() {
      this.microphone = !this.microphone
    }
  },
  mounted() {
    this.join()
    this.$refs.webrtc.onUserJoined = this.onUserJoined
  }
}
</script>

<style scoped></style>
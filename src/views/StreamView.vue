<template>
  <div class="bg-grey-darken-4" style="height: 100vh;">
    <v-row class="ma-0" style="height: 100%;">
      <v-col cols="12" md="9" class="bg-grey-darken-3"
        style="display: flex; flex-direction: column; justify-content: space-between;">

        <!-- Video -->
        <div id="video" class="bg-grey w-100 d-flex justify-center align-center pa-5">
          <vue-webrtc ref="webrtc" width="100%" roomId="sample-room" @joined-room="onUserJoined" @left-room="onUserLeft"
            @opened-room="onOpened" @share-started="onShareStarted" @share-stopped="onShareStopped" @enableVideo="stream"
            @enableAudio="microphone" @error="onError">
          </vue-webrtc>
        </div>

        <!-- Images -->
        <div v-if="img">
          <h2>Olingan rasm</h2>
          <figure class="figure">
            <img :src="img" class="figure-img img-fluid rounded" alt="Responsive image" />
          </figure>
        </div>

        <!-- Actions -->
        <div id="actions" class="d-flex justify-center pa-2 align-center">
          <v-btn class="mx-2" variant="outlined" :icon="stream ? 'mdi-video' : 'mdi-video-off'"
            @click="videoToggle"></v-btn>
          <v-btn class="mx-2" variant="outlined" :icon="microphone ? 'mdi-microphone' : 'mdi-microphone-off'"
            @click="microphoneToggle"></v-btn>
          <v-btn class="mx-2" variant="outlined" icon="mdi-close" @click="leave()" color="red"></v-btn>
          <v-btn class="mx-2" variant="outlined" icon="mdi-camera-outline" @click="onCapture"></v-btn>
          <v-btn class="mx-2" variant="outlined" icon="mdi-monitor-share" @click="onShareScreen"></v-btn>
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
      this.$router.push('/')
    },
    onUserJoined(user) {
      const newUser = {
        id: user,
        name: 'User'
      }
      this.users.push(newUser)
      console.log('onUserJoined', user)
    },
    onUserLeft(user) {
      console.log('onUserLeft', user)
    },
    onOpened(event) {
      console.log('onOpened: ', event)
    },
    onShareStarted(event) {
      console.log('onShareStarted: ', event)
    },
    onShareStopped(event) {
      console.log('onShareStopped: ', event)
    },
    onError(error, stream) {
      console.log('onError Event: ', error, "Stream: ", stream)
    },
    onCapture() {
      this.img = this.$refs.webrtc.capture()
    },
    onShareScreen() {
      this.img = this.$refs.webrtc.shareScreen();
    }

    // videoToggle() {
    //   this.stream = !this.stream
    // },
    // microphoneToggle() {
    //   this.microphone = !this.microphone
    // }
  },
  mounted() {
    this.join()
  }
}
</script>

<style scoped></style>
<template>
  <main class="h-screen d-flex justify-center align-center text-white bg-deep-purple-darken-4">
    <!-- <v-btn class="ma-2" color="grey-light text-capitalize" @click="$router.push('/admin')">Create Stream</v-btn> -->

    <div class="d-flex flex-column text-center" style="width: 300px;">
      <v-text-field class="ma-2 text-capitalize " label="Room ID" v-model="roomId" variant="solo" />
      <v-btn class="ma-2 text-white text-capitalize " color="green-darken-2" @click="joinRoom">Join
        Stream</v-btn>
    </div>
  </main>
</template>

<script>
export default {
  data() {
    return {
      roomId: 'public-room',
    }
  },
  methods: {
    joinRoom() {
      this.$router.push(`/stream/${this.roomId}`)
    }
  }
}
</script>

<style scoped></style>
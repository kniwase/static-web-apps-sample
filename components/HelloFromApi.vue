<template>
  <div>
    Message From Api: <strong>{{ message }}</strong>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "nuxt-property-decorator";
import axios from "axios";

@Component
export default class HelloFromApi extends Vue {
  message: string = "";
  async mounted() {
    this.message = await this.getMessage();
  }
  async getMessage(): Promise<string> {
    try {
      const res = await axios.get("/api/hello");
      const message: string = res.data.text;
      console.log(message);
      return message;
    } catch (error) {
      console.error(error);
      return "";
    }
  }
}
</script>
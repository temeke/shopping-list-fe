<template>
  <div id="app">
    <h1>Shopping List Interpreter</h1>
    <textarea v-model="userInput" placeholder="Write or speak your thoughts about the sopping list here..."></textarea>
    <button @click="sendToBackend">Send</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userInput: ''
    };
  },
  methods: {
    async sendToBackend() {
      try {
        const response = await fetch('http://localhost:3000/process', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({ text: this.userInput }),
        });
        if (!response.ok) throw new Error('Error while sending data');
        const data = await response.json();
        console.log(data);
      } catch (error) {
        console.error('Error:', error);
      }
    }
  }
};
</script>
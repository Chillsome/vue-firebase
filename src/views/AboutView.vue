<template>
  <div class="about">
    <span>
      <h1>Chat GPT</h1>
      <form @submit.prevent="submit">
        <input v-model="prompt" placeholder="Ask me" />
        <button type="submit">Submit</button>
      </form>
      <div v-if="response">{{ response }}</div>
    </span>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      response: null,
      // Add your OpenAI API key here
      apiKey: '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',
      // Add the endpoint for GPT-3 API
      gptEndpoint: 'https://api.openai.com/v1/engines/davinci/completions',
      // Set the prompt for the AI
    };
  },
  methods: {
    async submit() {
      try {
        const headers = {
          'Content-Type': 'application/json',
          Authorization: `Bearer ${this.apiKey}`,
        };

        const data = {
          prompt: this.prompt,
          max_tokens: 100, // Set the desired token limit
        };

        const response = await axios.post(this.gptEndpoint, data, { headers });
        this.response = response.data.choices[0].text.trim();
      } catch (error) {
        console.error('Error fetching data:', error);
        this.response = 'Error fetching data';
      }
    },
  },
};
</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>

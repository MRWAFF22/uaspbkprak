<template>
    <div class="photo-widget">
      <h2>{{ title }}</h2>
      <div class="photo-container">
        <img :src="photoUrl" :alt="title" />
      </div>
      <button @click="getRandomPhoto">Load New Photo</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        title: '',
        photoUrl: '',
      };
    },
    mounted() {
      this.getRandomPhoto();
    },
    methods: {
      async getRandomPhoto() {
        try {
          const apiKey = '38037020-2c48722c03be8437a05b588e6';
          const apiUrl = `https://pixabay.com/api/?key=${apiKey}&q=music+album&image_type=photo&orientation=horizontal`;
  
          const response = await fetch(apiUrl);
          const data = await response.json();
  
          const randomIndex = Math.floor(Math.random() * data.hits.length);
          const randomPhoto = data.hits[randomIndex];
  
          this.title = randomPhoto.tags;
          this.photoUrl = randomPhoto.webformatURL;
        } catch (error) {
          console.error('Error fetching random photo:', error);
        }
      },
    },
  };
  </script>
  
  <style scoped>
  .photo-widget {
    background-color: cornflowerblue;
    border: 1px solid #ccc;
    padding: 20px;
    margin-bottom: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  .photo-widget h2 {
    color: white;
  }
  
  .photo-container {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    max-width: 500px;
    margin-top: 10px;
  }
  
  .photo-container img {
    max-width: 100%;
    max-height: 100%;
  }
  
  .photo-widget button {
    margin-top: 10px;
  }
  </style>
  
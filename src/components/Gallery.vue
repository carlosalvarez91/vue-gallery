<template>
  <div class="gallery">
    <div class="gallery-panel"
         v-for="photo in photos"
         :key="photo.id">
        <a :href="photo.url" target="_blank">
            <img :src="photo.download_url">
            <div class="img-footer">
            {{photo.author}}
            </div>
        </a>
      
    </div>
  </div>
</template>

<script>

export default {
  name: 'Gallery',
  props:{
      photos: Array
  }
};
</script>

<style>
  .gallery {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(20rem, 1fr));
    grid-gap: 1rem;
    max-width: 80rem;
    margin: 2rem auto;
    padding: 0 5rem;
  }
  .gallery-panel{
      background: #ffffff;
  }
   a{
        text-decoration: none;
    }
  .gallery-panel .img-footer{
      height: 28px;
      color:#2c2c2c;
    }

  .gallery-panel img {
    width: 100%;
    height: 22vw;
    object-fit: cover;
  }
</style>
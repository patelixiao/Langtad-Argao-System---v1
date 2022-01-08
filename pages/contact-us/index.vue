<template>
  <div>
    <div class="hero-section w-full">
      <div class="banner-container relative h-screen w-full">
        <div class="image-div absolute top-0 left-0 h-full w-full">
          <img src="uploads/img/banner_1.jpg" class="w-full h-full object-cover">
        </div>
        <div class="relative z-50 content-div w-full h-full bg-black bg-opacity-80 flex">
          <div class="title block m-auto">
            <h1 class="text-6xl text-white uppercase">Langtad Argao Cebu</h1>
          </div>
        </div>
      </div>
    </div>
    <div class="header-navigation bg-blue-300 py-2 px-5">
      <div class="logo-container">
        <Navigations/>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    head: {
    title: 'Contact Us - Langtad Argao',
    meta: [
      { charset: 'utf-8' },
      { name: 'viewport', content: 'width=device-width, initial-scale=1' },
      {
        hid: 'description',
        name: 'description',
        content: 'Langtad is a barangay in the municipality of Argao, in the province of Cebu. Its population as determined by the 2020 Census was 3,417. This represented 4.37% of the total population of Argao.'
      }
    ],
    link: [{ rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' }]
  }
}
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,400;0,900;1,100;1,400;1,900&display=swap');

*{
  font-family: 'Roboto', sans-serif;
}
</style>
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
    <div class="body-div">
      <div class="about-langtad-home relative">
        <div class="relative max-w-4xl m-auto my-10 flex flex-wrap">
          <div class="w-3/5 relative p-10">
            <div class="img">
              <img src="uploads/img/banner_1.jpg" class="overflow-hidden rounded-md shadow-md"/>
            </div>
          </div>
          <div class="w-2/5 relative my-10">
            <div class="history absolute top-0 left-0">
              <h2 class="text-9xl font-bold text-gray-100">History</h2>
            </div>
            <div class="title relative pt-10">
              <h2 class="text-5xl font-bold uppercase">About Langtad</h2>
              <p>Langtad is a barangay in the municipality of Argao, in the province of Cebu. Its population as determined by the 2020 Census was 3,417. This represented 4.37% of the total population of Argao.</p>
              <p>The household population of Langtad in the 2015 Census was 3,145 broken down into 695 households or an average of 4.53 members per household.</p>
            </div>
          </div>
        </div>
      </div>
      <!-- about-langtad-home class closing -->
    </div>
  </div>
</template>
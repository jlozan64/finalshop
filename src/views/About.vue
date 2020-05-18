<template>
  <div>
    <div
      class="relative h-screen w-screen bg-cover bg-center shadow-2xl"
      :style="`background-image:url(${bgImage})`"
    >
      <div class="h-screen w-screen bg-purple-800 opacity-75" />
      <div
        class="absolute h-screen w-screen top-0 flex flex-col justify-center items-center"
      >
        <h2
          class="text-4xl font-bold text-white px-4 hover:bg-white hover:text-pink-800 opacity-75"
        >
         Our Little Shop
        </h2>
        <h3
          class="text-2xl font-bold text-white px-4 hover:bg-white hover:text-pink-800 opacity-75"
        >
         Located in Rio Grande Valley, Tina's Pastery Shop crafts all of our baked treats from scratch with fresh and natural ingredients.
For the most discerning sweet tooth, we offer ready to go Cakes, Cupcakes, Cake Pops, French Macarons, Cookies, Pies, and much more! You can make a purchase through our website or visit our local shop!
        </h3>
      </div>
    </div>
  </div>
</template>

<script>
import bgImage from "../assets/bg.jpg";
export default {
  name: "about",
  data() {
    return {
      bgImage
    };
  }
};
</script>

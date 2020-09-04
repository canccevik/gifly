<template>
  <div>
      <Gifs title="🚀   Trending" query="trending"></Gifs>
      <Gifs title="🎲   Random Gifs" query="random" count=25></Gifs>
      <Gifs title="🐶   Animals" query="search?q=animal"></Gifs>
      <Gifs title="⭐   Space" query="search?q=space"></Gifs>
      <Gifs title="🌲   Nature" query="search?q=nature"></Gifs>
  </div>
</template>

<script>
import Gifs from '../components/Gifs';

export default {
    name: "Home",
    components: { Gifs },
}
</script>
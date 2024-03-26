<template>
  <section :style="{'background-image': `url(${currentImg.url})`}" class="min-h-screen">
    <svg style="fill: white" viewBox="0 0 22 22" width="22" height="22" class="absolute z-10 top-[calc(50%_-_11px)] left-[calc(50%_-_11px)]">
      <polygon points="22 11.751 0 11.751 0 10.249 22 10.249 22 11"></polygon>
      <polygon points="11.751 0 11.751 22 10.249 22 10.249 0 11 0"></polygon>
    </svg>

    <button @click="router.back()" class="fixed z-[9995] top-[37px] left-[40px] text-[16px] text-white hover:text-[#00bd7e] leading-5 overflow-hidden transition-colors duration-300">Back</button>

    <ul
      id="image-slider"
      data-mouse-down-at="0"
      data-prev-percentage="0"
      class="flex gap-[4vmin] absolute left-[calc(50%_-_20vmin)] top-1/2 translate-x-0 -translate-y-1/2 select-none"
      :class="{'transfered': currentImg}"
    >
      <li v-for="img in imgs" :key="img.id">
        <img
          :src="img.url"
          :alt="img.id"
          class="max-w-none w-[40vmin] h-[56vmin] object-cover object-[100%_center]"
          draggable="false"
          @click="increaseImg(img)"
        />
        <!-- class for scale -->
        <!-- :class="currentImg.id === img.id ? 'scaleImg' : 'reduceImg'" -->
      </li>
    </ul>
  </section>
</template>

<script setup lang="js">
import { onMounted, ref } from 'vue'
import router from '../router'

const imgs = ref([
  {
    id: 1,
    url: 'https://images.unsplash.com/photo-1620480923566-4515f800999e?q=80&w=1974&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'
  },
  {
    id: 2,
    url: 'https://images.unsplash.com/photo-1632681872076-f73c6493414a?q=80&w=2069&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'
  },
  {
    id: 3,
    url: 'https://images.unsplash.com/photo-1630484383171-fd6270cb9619?q=80&w=1931&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'
  },
  {
    id: 4,
    url: 'https://images.unsplash.com/photo-1610041429609-ca215c1d69b7?q=80&w=2012&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'
  },
  {
    id: 5,
    url: 'https://images.unsplash.com/photo-1610620746460-de78cf3d1705?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'
  },
  {
    id: 6,
    url: 'https://images.unsplash.com/photo-1553949345-eb786bb3f7ba?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'
  },
  {
    id: 7,
    url: 'https://images.unsplash.com/photo-1703244551612-96e72990d724?q=80&w=1979&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'
  },
  {
    id: 8,
    url: 'https://images.unsplash.com/photo-1626891108693-27b4ab2ec650?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D'
  }
])
const currentImg = ref('')
const increaseImg = (img) => {
  currentImg.value = currentImg.value.id === img.id ? '' : img
}

onMounted(() => {
  const track = document.getElementById('image-slider')
  const allImages = track.getElementsByTagName('img')

  const setMouseDownAt = (e) => {
    track.dataset.mouseDownAt = e.clientX
  }

  const moveSlider = (e, delta) => {
    if (track.dataset.mouseDownAt === '0') return
    const mouseDelta = delta || parseFloat(track.dataset.mouseDownAt) - e.clientX
    const maxDelta = window.innerWidth / 2

    const percentage = (mouseDelta / maxDelta) * -100
    const nextPercentageWithoutLimit = parseFloat(track.dataset.prevPercentage) + percentage
    // console.log('nextPercentageWithoutLimit :>> ', nextPercentageWithoutLimit)
    const nextPercentage = Math.max(Math.min(nextPercentageWithoutLimit, 0), -88)
    track.dataset.percentage = nextPercentage
    track.animate(
      {
        transform: `translate(${nextPercentage}%, -50%)`
      },
      { duration: 1200, fill: 'forwards' }
    )
    ;[...allImages].map((im) =>
      im.animate(
        {
          objectPosition: `${nextPercentage + 100}% 50%`
        },
        { duration: 1200, fill: 'forwards' }
      )
    )
  }

  const setEndPoint = () => {
    track.dataset.mouseDownAt = '0'
    track.dataset.prevPercentage = track.dataset.percentage
  }

  window.onmousedown = (e) => {
    setMouseDownAt(e)
  }

  window.onmousemove = (e) => {
    moveSlider(e)
  }

  window.onmouseup = () => {
    setEndPoint()
  }

  window.onwheel = (e) => {
    const delta = -e.wheelDelta / 6
    setMouseDownAt(e)
    moveSlider(e, delta)
    setEndPoint()
  }
})
</script>

<style scoped>
section {
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}
/* .transfered {
  bottom: 36px;
  right: 36px;
  z-index: 10;
} */
.scaleImg {
  width: 100vw;
    height: 100vh;
    transition: all 1.5s ease-in-out;
    z-index: 5;
}
.reduceImg {
  width: 40vmin;
    height: 56vmin;
    transition: all 1.5s ease-in-out;
}
/* position: absolute;
    top: -40%;
    left: -27.5%; */
</style>

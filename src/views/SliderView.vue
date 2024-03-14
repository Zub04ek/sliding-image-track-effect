<template>
  <svg style="fill: white" viewBox="0 0 22 22" width="22" height="22" class="absolute z-10">
    <polygon points="22 11.751 0 11.751 0 10.249 22 10.249 22 11"></polygon>
    <polygon points="11.751 0 11.751 22 10.249 22 10.249 0 11 0"></polygon>
  </svg>

  <ul
    id="image-slider"
    data-mouse-down-at="0"
    data-prev-percentage="0"
    class="flex gap-[4vmin] absolute left-[calc(50%_-_20vmin)] top-1/2 translate-x-0 -translate-y-1/2 select-none"
  >
    <li class="">
      <img
        class="max-w-none w-[40vmin] h-[56vmin] object-cover object-[100%_center]"
        src="https://images.unsplash.com/photo-1620480923566-4515f800999e?q=80&w=1974&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
        alt="1"
        draggable="false"
      />
    </li>
    <li class="">
      <img
        class="max-w-none w-[40vmin] h-[56vmin] object-cover object-[100%_center]"
        src="https://images.unsplash.com/photo-1632681872076-f73c6493414a?q=80&w=2069&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
        alt="2"
        draggable="false"
      />
    </li>
    <li class="">
      <img
        class="max-w-none w-[40vmin] h-[56vmin] object-cover object-[100%_center]"
        src="https://images.unsplash.com/photo-1630484383171-fd6270cb9619?q=80&w=1931&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
        alt="3"
        draggable="false"
      />
    </li>
    <li class="">
      <img
        class="max-w-none w-[40vmin] h-[56vmin] object-cover object-[100%_center]"
        src="https://images.unsplash.com/photo-1610041429609-ca215c1d69b7?q=80&w=2012&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
        alt="4"
        draggable="false"
      />
    </li>
    <li class="">
      <img
        class="max-w-none w-[40vmin] h-[56vmin] object-cover object-[100%_center]"
        src="https://images.unsplash.com/photo-1610620746460-de78cf3d1705?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
        alt="5"
        draggable="false"
      />
    </li>
    <li class="">
      <img
        class="max-w-none w-[40vmin] h-[56vmin] object-cover object-[100%_center]"
        src="https://images.unsplash.com/photo-1553949345-eb786bb3f7ba?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
        alt="6"
        draggable="false"
      />
    </li>
    <li class="">
      <img
        class="max-w-none w-[40vmin] h-[56vmin] object-cover object-[100%_center]"
        src="https://images.unsplash.com/photo-1703244551612-96e72990d724?q=80&w=1979&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
        alt="7"
        draggable="false"
      />
    </li>
    <li class="">
      <img
        class="max-w-none w-[40vmin] h-[56vmin] object-cover object-[100%_center]"
        src="https://images.unsplash.com/photo-1626891108693-27b4ab2ec650?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D"
        alt="8"
        draggable="false"
      />
    </li>
  </ul>
</template>

<script setup lang="js">
import { onMounted } from 'vue'

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

<style lang="scss" scoped></style>

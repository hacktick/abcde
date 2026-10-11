<script setup lang="ts">
import { onBeforeUnmount, onMounted, useTemplateRef } from 'vue'
import * as THREE from 'three'

const canvas = useTemplateRef<HTMLCanvasElement>('canvas')

let renderer: THREE.WebGLRenderer | undefined
let resizeObserver: ResizeObserver | undefined

onMounted(() => {
  const el = canvas.value
  if (!el) return

  renderer = new THREE.WebGLRenderer({ canvas: el, antialias: true })
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))

  const scene = new THREE.Scene()
  scene.background = new THREE.Color(0x12141c)

  const camera = new THREE.PerspectiveCamera(60, 1, 0.1, 100)
  camera.position.z = 3

  const cube = new THREE.Mesh(
    new THREE.BoxGeometry(1, 1, 1),
    new THREE.MeshStandardMaterial({ color: 0x42b883 }),
  )
  scene.add(cube)

  scene.add(new THREE.AmbientLight(0xffffff, 0.6))
  const light = new THREE.DirectionalLight(0xffffff, 2)
  light.position.set(2, 3, 4)
  scene.add(light)

  resizeObserver = new ResizeObserver(() => {
    const { clientWidth, clientHeight } = el
    renderer?.setSize(clientWidth, clientHeight, false)
    camera.aspect = clientWidth / clientHeight
    camera.updateProjectionMatrix()
  })
  resizeObserver.observe(el)

  const timer = new THREE.Timer()
  renderer.setAnimationLoop((time) => {
    timer.update(time)
    const delta = timer.getDelta()
    cube.rotation.x += delta * 0.6
    cube.rotation.y += delta * 0.9
    renderer?.render(scene, camera)
  })
})

onBeforeUnmount(() => {
  resizeObserver?.disconnect()
  renderer?.setAnimationLoop(null)
  renderer?.dispose()
})
</script>

<template>
  <canvas ref="canvas" class="game-canvas" />
</template>

<style scoped>
.game-canvas {
  position: fixed;
  inset: 0;
  width: 100%;
  height: 100%;
  display: block;
}
</style>

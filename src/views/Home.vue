<template>
  <div class="home">
    <transition name="toast">
      <Toast v-if="showToast" />
    </transition>

    <Todos @badValue="triggerToast" />
    <transition name="whatever">
      <div v-if="showP">Hello Ninjas</div>
    </transition>
    <button @click="showP = !showP">Toggle</button>
  </div>
</template>

<script>
import { ref } from 'vue'
import Toast from '../components/Toast'
import Todos from '../components/Todos'

export default {
  components: { Toast, Todos },
  setup() {
    const showToast = ref(false)
    const showP = ref(false)

    const triggerToast = () => {
      showToast.value = true;
      setTimeout(() => showToast.value = false, 3000)
    }

    return { showToast, triggerToast, showP }
  }
}
</script>

<style>

  /*TOAST*/
  /*
  .toast-enter-from, 
  .toast-leave-to {
    opacity: 0;
    transform: translateY(-60px)
  }

  .toast-enter-to, 
  .toast-leave-from {
    opacity: 1;
    transform: translateY(0)
  }

  .toast-enter-active, 
  .toast-leave-active{
    transition: all 1s ease;
  }
  */

  .toast-enter-active {
    animation: wooble 0.5s ease
  }
  .toast-leave-to {
    opacity: 0;
    transform: translateY(-60px)
  }
  .toast-leave-active {
    transition: all 0.5s ease
  }
  

  @keyframes wooble{
    0%{ opacity: 0; transform: translateY(-60px)}
    50%{ opacity: 0; transform: translateY(-60px) }
    60% {transform: translateX(8px)}
    70% {transform: translateX(-8px)}
    80% {transform: translateX(4px)}
    90% {transform: translateX(-4px)}
    100% {transform: translateX(0)}
  }

  /*EXAMPLE*/  

  .whatever-enter-from {
    opacity: 0;
  }
  .whatever-enter-to {
    opacity: 1;
  }
  .whatever-enter-active {
    transition: all 2s ease;
  }

  .whatever-leave-from {
    opacity: 1;
  }
  .whatever-leave-to {
    opacity: 0;
  }
  .whatever-leave-active{
    transition: all 2s ease;
  }

</style>
<template>
  <div class="about">

    <transition 
      appear 
      name="title"
      @before-enter="beforeEnter"
      @enter="enter"
      @after-enter="afterEnter"
      @before-leave="beforeLeave"
      @leave="leave"
      @after-leave="afterLeave"
    >
          <h1 v-if="showTitle">About</h1>
    </transition>


    <transition
      appear
      @before-enter="bfEnter"
      @enter="ent"
      @after-enter="afEnter"
    >
        <div>
          <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
          <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
          <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Cum aperiam officia possimus delectus inventore quod quisquam culpa voluptas iusto, quae maiores quo dolorum, corporis laboriosam a dolore consequatur assumenda nam!</p>
        </div>
    
    </transition>


  </div>
</template>

<script>
import {ref} from 'vue'
import gsap from 'gsap'

export default {
  setup() {

    const showTitle = ref(true)

    const bfEnter = (el)=>{

      el.style.transform = 'translateY(-60px)'
      el.style.opacity = 0

    }

    const ent = (el, done)=>{

      gsap.to(el, {
        duration: 1,
        y: 0, 
        opacity: 1, 
        ease: 'bounce-out', 
        onComplete: done
      })

    }

    const afEnter = ()=>{
      console.log('done')
    }

    const beforeEnter = (el)=>{
      console.log('before enter', el)
    }

    const enter = (el)=>{
      console.log('enter')
    }

    const afterEnter = (el)=>{
      console.log('after enter')
      el.style.color = 'green'

      setTimeout(()=>{
        showTitle.value = false;
      }, 2000)
    }

    const beforeLeave = (el)=>{
      console.log('before leave')
      el.style.color="red"
    }

    const leave = (el)=>{
      console.log('leave')
    }

    const afterLeave = (el)=>{
      console.log('after leave')
    }

    return {
      beforeEnter, enter, afterEnter, showTitle, beforeLeave, leave, afterLeave, ent, bfEnter, afEnter
    }

  }
}
</script>

<style>
  .about {
    max-width: 600px;
    margin: 20px auto;
  }

  .title-enter-from, 
  .title-leave-to{
    opacity: 0;
  }

  .title-enter-active, 
  .title-leave-active{
    transition: all 3s ease;
  }


</style>
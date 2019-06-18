<template>
  <div class="demo-contanner">
    <svg id="idea" version="1.1" xmlns="https://www.w3.org/2000/svg" xmlns:xlink="https://www.w3.org/<1999></1999>/xlink" width="349.698px" height="322.64px" viewBox="0 0 349.698 322.64" enable-background="new 0 0 349.698 322.64" xml:space="preserve">
      <defs>
        <filter id="glow" x="-50%" y="-50%" height="300%" width="300%">
          <feGaussianBlur stdDeviation="15" result="coloredBlur" />
          <feMerge>
            <feMergeNode in="coloredBlur" />
            <feMergeNode in="SourceGraphic" />
          </feMerge>
        </filter>
      </defs>
      <rect y="-9" width="350" height="10" />
      <g id="lampP" class="sB">
        <path
          class="lamp"
          filter="url(#glow)"
          fill="rgba(255,255,255,0.15)"
          d="M314.726,322.64c19.314,0,34.972-15.656,34.972-34.97c0-8.15-4.803-15.631-9.486-21.57 c-4.958-6.285-7.514-11.752-10.449-16.758h-30.069c-2.968,5.058-5.456,10.421-10.453,16.762 c-4.678,5.937-9.483,13.419-9.483,21.566C279.759,306.984,295.416,322.64,314.726,322.64z"
        />
        <line fill="none" stroke="#000000" stroke-width="4" stroke-miterlimit="10" x1="314.729" y1="217.962" x2="314.729" y2="0" />
        <line fill="none" stroke="#000000" stroke-width="7" stroke-linecap="round" stroke-miterlimit="10" x1="301.347" y1="242.868" x2="328.285" y2="242.868" />
        <line fill="none" stroke="#000000" stroke-width="7" stroke-linecap="round" stroke-miterlimit="10" x1="301.347" y1="233.019" x2="328.285" y2="233.019" />
        <line fill="none" stroke="#000000" stroke-width="7" stroke-linecap="round" stroke-miterlimit="10" x1="304.871" y1="223" x2="324.761" y2="223" />
        <line fill="none" stroke="#000000" stroke-width="7" stroke-linecap="round" stroke-miterlimit="10" x1="310.046" y1="218" x2="319.585" y2="218" />
        <path fill="none" stroke="rgba(255,255,255,0.3)" stroke-width="7" stroke-linecap="round" stroke-miterlimit="10" d="M314.816,310.331 c12.415,0,22.511-10.097,22.511-22.508" />
      </g>
      <text id="T" x="320" y="210" fill="white" font-family="arial" font-size="1em"> ▼ Drag this one</text>
    </svg>
  </div>
</template>

<script>
import { TweenLite } from 'gsap/TweenMax'
import Draggable from 'gsap/Draggable'

export default {
  name: 'BlogDemo',
  data() {
    return {
      timeline: null
    }
  },
  mounted() {
    const that = this
    const A = document.createElement('audio')
    A.src = 'http://www.freesound.org/data/previews/117/117697_646701-lq.mp3'
    A.volume = 0.5
    const Lamp = document.getElementById('lampP')
    const svg = document.getElementById('idea')
    for (let i = 1; i < 5; i++) {
      const newLamp = Lamp.cloneNode(true)
      svg.appendChild(newLamp)
      TweenLite.set(newLamp, {
        x: i * -70,
        className: i > 3 ? 'eB' : 'mB'
      })
    }
    TweenLite.set('.sB,.eB', {
      transformOrigin: '50% 0px'
    })
    const tl = new TimelineMax({
      paused: true,
      yoyo: true,
      onComplete: function() {
        TweenLite.to('.sB,.eB', 0.3, {
          rotation: 0,
          ease: Sine.easeIn,
          onComplete: AP
        })
        TweenLite.to('.sB .lamp,.eB .lamp', 0.3, {
          fill: 'rgba(255,255,255,0.15)'
        })
        TweenLite.to('.report', 1, {
          text: {
            value: 'Error #404 , New Ideas Not found !... pls try again'
          },
          delay: 0.3
        })
        D[0].enable()
        that.$emit('handleLogin')
      }
    })
    const T1 = TweenMax.fromTo('.sB', 0.3, {
      rotation: null
    }, {
      rotation: 0,
      ease: Sine.easeIn
    })
    const T2 = TweenMax.to('.eB', 0.3, {
      rotation: 0,
      ease: Sine.easeOut,
      immediateRender: true
    })
    tl.add(T1).to('.sB .lamp', 0.3, {
      fill: 'rgba(255,255,255,0.15)',
      ease: Elastic.easeOut.config(1, 0.5)
    }, 0)
      .staggerTo('.mB .lamp', 0.01, {
        fill: 'white',
        repeat: 1,
        yoyo: true
      }, 0.025)
      .add(T2).to('.eB .lamp', 0.3, {
        fill: 'white',
        ease: Elastic.easeIn.config(1, 0.5)
      }, '-=0.3')
      .add(AP, '-=0.35')
    const D = Draggable.create('.sB', {
      type: 'rotation',
      bounds: {
        minRotation: -70
      },
      onPress: function() {
        TweenLite.to('#T', 0.3, {
          fill: 'rgba(0,0,0,0)'
        })
        TweenLite.set('.sB .lamp', {
          fill: 'white'
        })
      },
      onDragEnd: PU
    })

    function PU() {
      const X = this.rotation
      this.disable()
      T1.vars.startAt.rotation = X
      T2.vars.css.rotation = -X
      tl.seek(0).invalidate().restart().repeat(R(3, 15))
    }

    function AP() {

    }

    function R(min, max) {
      return min + Math.floor(Math.random() * (max - min))
    }

    /* a Pen by DIACO : twitter.com/Diaco_ml || codepen.io/MAW */
  },
  methods: {

  }
}
</script>

<style lang="scss" scoped>
.demo-contanner {
  display: flex;
  align-items: center;
}
svg {
  margin: auto;
  overflow: visible;
}
.sB {
  cursor: pointer;
}
</style>

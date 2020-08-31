<template>
  <div class="container">
    <div class="text">枠の中に図形を移動できます</div>
    <!-- SVG定義 -->
    <svg>
      <rect v-for="(r, idx) in rects" :key="idx"
        @mousedown="move($event, idx)"
        :fill="r.color" :stroke="r.stroke"
        :rx="r.rx"
        :x="r.x" :y="r.y" :width="r.w" :height="r.h">{{message}}
      </rect>
      <rect stroke="darkblue" stroke-width="5" fill="none" 
      x="600" :y="100" :width="300" :height="300">
      </rect>
    </svg>
  </div>
</template>

<script>
export default {
  name: 'SVGDemo',
  data () {
    return {
      ratio: 1,
      dx: 0,
      dy: 0,
      viewport: '0 0 500 500',
      isMove: false,
      beforeMouseX: null,
      beforeMouseY: null,
      selectIdx: 0,
      rects: [
        {
          x: 10,
          y: 10,
          w: 100,
          h: 100,
          id: "green",
          color: 'green',
          stroke: 'black',
        },
        {
          x: 200,
          y: 150,
          w: 100,
          h: 100,
          color: 'red',
          stroke: 'black',
        },
        {
          x: 310,
          y: 410,
          w: 200,
          h: 100,
          color: 'blue',
          stroke: 'black',
        },
        {
          x: 100,
          y: 200,
          w: 200,
          h: 100,
          color: 'yellow',
          stroke: 'black',
        },
        {
          x: 300,
          y: 300,
          w: 50,
          h: 50,
          color: 'skyblue',
          stroke: 'black',
        },
        {
          x: 280,
          y: 280,
          w: 50,
          h: 50,
          color: 'white',
          stroke: 'black',
        },
        {
          x: 300,
          y: 300,
          w: 50,
          h: 50,
          color: 'pink',
          stroke: 'black',
        },
        {
          x: 150,
          y: 300,
          w: 50,
          h: 50,
          color: 'lightgreen',
          stroke: 'black',
        },
        {
          x: 50,
          y: 400,
          w: 200,
          h: 50,
          color: 'black',
          stroke: 'black',
        },
        {
          x: 50,
          y: 450,
          w: 200,
          h: 50,
          color: 'brown',
          stroke: 'black',
        },
      ]
    } 
  },
  // マウス操作関連
  mounted () {
    console.log('MOUNT LISTENER ON')
    document.addEventListener('mouseup', this.mouseUp)
    document.addEventListener('mousemove', this.mouseMove)
  },
  beforeDestroy () {
    console.log('MOUNT LISTENER OFF')
    document.removeEventListener('mouseup', this.mouseUp)
    document.removeEventListener('mousemove', this.mouseMove)
  },
  methods: {
    
    // 図形を動かすフラグを立てる
    move (e, i) {
      this.isMove = true
      this.selectIdx = i
      e.preventDefault()
    },
    // マウスのクリックが終わった段階で初期化
    mouseUp (e) {
      this.isMove = false
      this.beforeMouseX = null
      this.beforeMouseY = null
      e.preventDefault()
    },
    // move中は前回まで動かした差分を取りながら座標を変化させていく
    mouseMove (e) {
      if (!this.isMove) return
      var mouseX = e.offsetX * this.ratio + this.dx
      var mouseY = e.offsetY * this.ratio + this.dy
      var dx = 0
      var dy = 0
      if (this.beforeMouseX && this.beforeMouseY) {
          dx = mouseX - this.beforeMouseX
          dy = mouseY - this.beforeMouseY
      }
      this.beforeMouseX = mouseX
      this.beforeMouseY = mouseY
      var tempX = dx + Number(this.rects[this.selectIdx].x)
      var tempY = dy + Number(this.rects[this.selectIdx].y)
      //var tempX = dx + Number(this.polygons[this.selectIdx].x)
      //var tempY = dy + Number(this.polygons[this.selectIdx].y)
      if (tempX > 0) this.rects[this.selectIdx].x = tempX
      if (tempY > 0) this.rects[this.selectIdx].y = tempY
      e.preventDefault()
    }
  },
  
}
</script>

<style>
.text {
  font-size:35px;
}
svg {
  width : 1000px;
  height: 500px;
  background-color: silver;
  polygon {
    background-color: black;
    fill: black;
  }
}
polygon {
  background-color: black;
  fill: black;
}

</style>
<template>
  <div id="div-demo">
    <div>
      <label>背景图效果:</label>
      <div :style="demo1Style">
        <p class="div-demo-1-text">
          Hippy 背景图展示
        </p>
      </div>
      <label>渐变色效果:</label>
      <div class="div-demo-1-1">
        <p class="div-demo-1-text">
          Hippy 背景渐变色展示
        </p>
      </div>
      <label>Transform</label>
      <div class="div-demo-transform">
        <p class="div-demo-transform-text">
          Transform
        </p>
      </div>
      <label>水平滚动:</label>
      <div
        ref="demo-2"
        class="div-demo-2"
        :scrollEnabled="true"
        :pagingEnabled="false"
        :showsHorizontalScrollIndicator="false"
        @scroll="onScroll"
        @momentumScrollBegin="onMomentumScrollBegin"
        @momentumScrollEnd="onMomentumScrollEnd"
        @scrollBeginDrag="onScrollBeginDrag"
        @scrollEndDrag="onScrollEndDrag"
      >
        <!-- div 带着 overflow 属性的，只能有一个子节点，否则终端会崩溃 -->
        <div class="display-flex flex-row">
          <p class="text-block">
            A
          </p>
          <p class="text-block">
            B
          </p>
          <p class="text-block">
            C
          </p>
          <p class="text-block">
            D
          </p>
          <p class="text-block">
            E
          </p>
        </div>
      </div>
      <label>垂直滚动:</label>
      <div
        class="div-demo-3"
        :showsVerticalScrollIndicator="false"
      >
        <!-- div 带着 overflow 属性的，只能有一个子节点，否则终端会崩溃 -->
        <div class="display-flex flex-column">
          <p class="text-block">
            A
          </p>
          <p class="text-block">
            B
          </p>
          <p class="text-block">
            C
          </p>
          <p class="text-block">
            D
          </p>
          <p class="text-block">
            E
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import defaultImage from '../../assets/defaultSource.jpg';

export default {
  data() {
    /**
     * demo1 needs to use variable base64 DefaultImage，so inline style mode is a must.
     * if image path is remote address, declaration style class .div-demo-1 can be used.
     */
    return {
      demo1Style: {
        display: 'flex',
        height: '40px',
        width: '200px',
        /**
         *  inline style 'backgroundImage': `url(${DefaultImage})` with 'url()' syntax only supported above 2.6.1.
         *  declaration css style supports 'background-image': `url('https://xxxx')` format and remote address only.
         */
        backgroundImage: `${defaultImage}`,
        backgroundRepeat: 'no-repeat',
        justifyContent: 'center',
        alignItems: 'center',
        marginTop: '10px',
        marginBottom: '10px',
      },
    };
  },
  mounted() {
    this.demon2 = this.$refs['demo-2'];
    setTimeout(() => {
      this.demon2.scrollTo(50, 0, 1000);
    }, 1000);
  },
  methods: {
    onScroll(e) {
      console.log('onScroll', e);
    },
    onMomentumScrollBegin(e) {
      console.log('onMomentumScrollBegin', e);
    },
    onMomentumScrollEnd(e) {
      console.log('onMomentumScrollEnd', e);
    },
    onScrollBeginDrag(e) {
      console.log('onScrollBeginDrag', e);
    },
    onScrollEndDrag(e) {
      console.log('onScrollEndDrag', e);
    },
  },
};
</script>

<style scoped>

  /* Common CSS Styles */

  #div-demo {
    flex: 1;
    overflow-y: scroll;
  }

  .display-flex {
    display: flex;
  }

  .flex-row {
    flex-direction: row;
  }

  .flex-column {
    flex-direction: column;
  }

  .text-block {
    width: 100px;
    height: 100px;
    line-height: 100px;
    border-style: solid;
    border-width: 1px;
    border-color: #40b883;
    font-size: 80px;
    margin: 20px;
    color: #40b883;
    text-align: center;
  }

  /* background-image path can only use remote address */
  /*.div-demo-1 {*/
  /*  display: flex;*/
  /*  height: 40px;*/
  /*  background-image: url('http://mat1.gtimg.com/www/qq2018/imgs/qq_logo_2018x2.png');*/
  /*  background-repeat: no-repeat;*/
  /*}*/

  .div-demo-1-1 {
    display: flex;
    height: 40px;
    width: 200px;
    background-image: linear-gradient(30deg, blue 10%, yellow 40%, red 50%);
    border-width: 2px;
    border-color: black;
    border-radius: 2px;
    justify-content: center;
    align-items: center;
    margin-top: 10px;
    margin-bottom: 10px;
  }

  .div-demo-1-text {
    color: white;
    margin-left: 10px;
  }

  /* flex-direction is necessary for horizontal scrolling for Native */
  .div-demo-2 {
    overflow-x: scroll;
    margin: 10px;
    flex-direction: row;
  }

  .div-demo-3 {
    overflow-y: scroll;
    margin: 10px;
    height: 320px;
  }

  .div-demo-transform {
    background-color: #40b883;
    transform: rotate(30deg) scale(.5);
    width: 120px;
    height: 120px;
  }

  .div-demo-transform-text {
    line-height: 120px;
    height: 120px;
    width: 120px;
    text-align: center;
  }
</style>

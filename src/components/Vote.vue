<template>
  <div>
    <h3 ref="root">{{title}}</h3>
    <div>
      <p>support: {{supNum}}</p>
      <p>against: {{oppNum}}</p>
      <p>radio: {{radio}}</p>
      <button @click="change(0)">supportion</button>
      <button @click="change(1)">Opposition</button>
    </div>
  </div>
</template>
<script>
import { watchEffect, ref, reactive, toRefs, readonly, computed, watch, onMounted } from 'vue'
  export default {
    props: {
      title: String
    },
    // 初始化props和beforeCreate之间 处理setup
    setup(props) {
      // props: 基于Proxy代理的响应式数据
      //1 构建响应式数据 ref (一般处理简单值的响应式) 基于Object.defineProperty
      // let supNum = ref(0), oppNum = ref(0)
      /* let state = ref({
        supNum: 0,
        oppNum: 0,
      }) */


      // 2 构建响应式数据 reactive (基于 Proxy 对数据进行深度监听)
      let state = reactive({
        supNum: 0,
        oppNum: 0,
      })

      //3 toRefs 将reactive重的每一项变为ref响应式数据
      // console.log(toRefs(state))


      //4 readonly
      let a = reactive({
        x: 11,
        y: {
          z: 344,
        }
      })
      let b = readonly(a)
      // b.y.z = 111 // warn Set operation on key "z" failed: target is readonly.


      //5 computed
      // let radio = computed(() => {
      //   let total = state.supNum + state.oppNum
      //   return total === 0 ? '--' : `${((state.supNum / total) * 100).toFixed(2)}%`
      // })
      // radio = 300 //改变指针
      // radio.value++ // warn vue.js:982 Write operation failed: computed value is readonly

      /* let radio = computed({
        get: () => {
          let total = state.supNum + state.oppNum
          return total === 0 ? '--' : `${((state.supNum / total) * 100).toFixed(2)}%`
        },
        set: val => {
          console.log('set', val)
        }
      }) */
      // radio.value = 100


      //6 watchEffect
      /* watchEffect(() => {
        console.log('watchEffect: ', state.supNum)
      }) */

      //7 watch
      /* watch(state, () => {
        console.log('watch: ', state.supNum)
      }) */

      /* watch(() => state.supNum, () => {
        console.log('watch: ', state.supNum)
      }) */

      // let x = ref(0), y = ref(0)
      /* watch(x, (x, prex) => {
        console.log(x, prex)
      }) */
      /* watch([x, y], ([x, y], [prex, prey]) => {
        console.log(x, prex)
      }) */


      const change = (lx) => {
        lx === 0 ? state.supNum++ : state.oppNum++
        // x.value++
      }

      let radio = ref('--')
      watch(state, state => {
        let total = state.supNum + state.oppNum
        radio.value =
         total === 0 ? '--' : `${((state.supNum / total) * 100).toFixed(2)}%`
      })

      // refs
      let root = ref(null)
      onMounted (() => {
        console.log(root.value)
      })

      return {
        ...toRefs(state),
        radio,
        root,
        change
      }
    }
  }
</script>

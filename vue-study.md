## vue-study project 만들기_0605

### 0_ markup 파일 추가 
***

### 1_ Vue Component 만들기
* 사용할 component >> App.vue 파일에 script 추가
```
<script>
import Header from './components/Header.vue'
import Nav from './components/Nav.vue'
import Footer from './components/Footer.vue'

export default {
  components: {
    Header,
    Nav,
    Footer
  }
}
</script>
```

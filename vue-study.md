## vue-study project 만들기_0605

### 0_ markup 파일 추가 
***

### 1_ Vue Component 만들기
* 사용할 component >> App.vue 파일에 script 추가
```html
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
* 사용할 component >> 파일 생성
<img width="222" alt="스크린샷 2021-06-06 18 38 26" src="https://user-images.githubusercontent.com/79742210/120919887-f33c4580-c6f6-11eb-9a59-85b23ca98536.png">

* App.vue >> Component로 분류
<img width="1157" alt="스크린샷 2021-06-06 18 27 29" src="https://user-images.githubusercontent.com/79742210/120919923-33032d00-c6f7-11eb-8249-11dbe9a0a50c.png">

* 만든 Component 모두 분류
<img width="530" alt="스크린샷 2021-06-06 18 29 13" src="https://user-images.githubusercontent.com/79742210/120919974-5201bf00-c6f7-11eb-99b0-98825f0bec9f.png">

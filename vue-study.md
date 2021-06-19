## vue-study project 만들기_0605

### 0_ markup 파일 추가 
***

### 1_ Vue Component 만들기
* Component >> 화면의 영역을 일정한 단위로 쪼개서 활용 가능한 형태로 관리
* 사용할 Component >> App.vue 파일에 script 추가
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
* 사용할 Component >> 파일 생성
<img width="222" alt="스크린샷 2021-06-06 18 38 26" src="https://user-images.githubusercontent.com/79742210/120919887-f33c4580-c6f6-11eb-9a59-85b23ca98536.png">

* App.vue >> Component로 분류
<img width="1157" alt="스크린샷 2021-06-06 18 27 29" src="https://user-images.githubusercontent.com/79742210/120919923-33032d00-c6f7-11eb-8249-11dbe9a0a50c.png">

* 만든 Component 모두 분류
<img width="530" alt="스크린샷 2021-06-06 18 29 13" src="https://user-images.githubusercontent.com/79742210/120919974-5201bf00-c6f7-11eb-99b0-98825f0bec9f.png">


### 2_ v-show/ v-if/ props
* v-show >> html display 속성 / none = 'false'
* v-if >> if문 / True 값일 때만 보여줌
```html
<Header v-show="true"></Header>
<Nav v-if="true"></Nav>
```

* props >> 부모 component에서 자식 component로 값 전달
```html
- 특정한 명령이 없다면 자식 compnent가 가지고 있는 'Copyright'라는 값을 불러옴
<Footer :title="'copy'"></Footer>
```
```html
<script>
export default {
  props: {
    title: {
      default: 'Copyright'
    }
  }
}
</script>
```

### 3_ Vue Router
* single page application >> 같은 화면에서 보여주는 화면을 변화시키면서 그려줌(화면전환) >> 바뀌면서 그려주는 부분 >> router-view
* Header / Nav(body) / Footer >> Nav 부분 == Router
```js
import Members from '../components/contents/Members.vue'
import Search from '../components/contents/Search.vue'

Vue.use(VueRouter)

const routes = [
  { path: '/', redirect: '/members' },
  {
    path: '/members',
    name: 'Members',
    component: Members
  },
  {
    path: '/search',
    name: 'Search',
    component: Search
  }
]
```


### 4_ Members Store 만들기
* Component가 바라보고 있는 함수 등의 약속들! > 따라서 store 안의 값이 바뀌면 바라보고 있는 Component들의 값도 바뀜 

- store 생성
* src/store/moduleMembers.js
```js
export const moduleMembers = {
  state: {
    members: [],
    member: {
      name: '',
      age: ''
    }
  },
  mutations: {
  },
  actions: {
    membersCreate(thisStore) {
      thisStore.state.members.push({
        name: thisStore.state.member.name,
        age: thisStore.state.member.age
      })
      console.log('Done membersCreate', moduleMembers.state.members)
    }
  }
}
```
* 그리고 생성한 store파일 /index.js 에 import & export
<img width="457" alt="스크린샷 2021-06-14 01 34 33" src="https://user-images.githubusercontent.com/79742210/121815327-dbddf900-ccb0-11eb-98f3-27cc241a5aaa.png">

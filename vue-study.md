## vue-study project 만들기

### 0_ markup 파일 추가(html+css)
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
* Header / Contents(body) / Footer >> Contents 부분 == Router
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
* 활성화시킬 텍스트에 link 붙이기 >> html 'a' 태그의 역할
```html
<li><h2><router-link :to="{name: 'Members'}" active-class="active">Members</router-link></h2></li>
<li><h2><router-link :to="{path: '/search'}" active-class="active">Search</router-link></h2></li>
```

### 4_ Members Store CRUD
#### Create
* Component가 바라보고 있는 함수 등의 약속들! > 따라서 store 안의 값이 바뀌면 바라보고 있는 Component들의 값도 바뀜(==html)
* store >> red project 에서 js의 역할(==javascript)
* store 생성
  - src/store/moduleMembers.js
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
  - 그리고 생성한 store파일 /index.js 에 import & export
  - js에서 'script'태그로 라이브러리 추가하는거랑 비슷한 원리
<img width="457" alt="스크린샷 2021-06-14 01 34 33" src="https://user-images.githubusercontent.com/79742210/121815327-dbddf900-ccb0-11eb-98f3-27cc241a5aaa.png">

* Inject components
  - src/components/contents/Members.vue


```js
<template>
  <div>
    <h3>Members</h3>
    <hr class="d-block" />
    <div>
      <h4>Read</h4>
      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Age</th>
            <th>Modify</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>홍길동</td>
            <td>20</td>
            <td>
              <button>Update</button>
              <button>Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <hr class="d-block" />
    <div>
      <h4>Create</h4>
      <input type="text" placeholder="Name" v-model="member.name" />
      <input type="text" placeholder="Age" v-model="member.age" />
      <button @click="membersCreate()">Create</button>
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    member() {
      return this.$store.state.members.member
    }
  },
  methods: {
    membersCreate() {
      this.$store.dispatch('membersCreate')
    }
  },
  created() {
    this.member.name = ''
    this.member.age = ''
  }
}
</script>

```

#### Read
* Read = mutations/actions를 js에! create가 아니기 때문에 !state
* js에는 membersRead가 불러올 값, 역할을 적어줌
  - src/store/moduleMembers.js
```js
  mutations: {
    membersRead(state, members) {
      state.members = members
    }
  actions: {
    membersRead(thisStore) {
      const members = [{
        name: '홍길동',
        age: 20
      }, {
        name: '춘향이',
        age: 16
      }]
      thisStore.commit('membersRead', members)
      console.log('Done membersRead', moduleMembers.state.members)
    }

```
* components에는 수기값을 빼고 index를 이용하여 접근할 수 있는 경로를 적어줌
  - src/components/contents/Memebers.vue
```js
<tr v-for="(member, index) in members" :key="index">
  <td>{{member.name}}</td>
  <td>{{member.age}}</td>

```
```js
export default {
  computed: {
    members() {
      return this.$store.state.members.members
    }
  created() {
    this.$store.dispatch('membersRead')
```

#### Update
* js >> actions에 불러올 update 역할 추가
  - src/store/moduleMembers.js
```js
  actions: {
    membersUpdate(thisStore, memberUpdate) {
      thisStore.state.members[memberUpdate.index] = memberUpdate.member
      console.log('Done membersUpdate', moduleMembers.state.members)
    }
```


#### Delete

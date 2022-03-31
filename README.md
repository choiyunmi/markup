
** vue 셋팅 명령어 **
it clone <원격 저장소 URL> sample2
git commit -m "change logic" 
git pull origin master
git init
npm install vue-cli -global  (vue2버전)
vue create 폴더명
npm run serve
vue add vuetify
vue add router

** 전역컴포넌트 등록을 위한 todo-footer 태그 추가  **
[app.js file]
Vue.component('todo-footer', {
    template: '<p>This is another global child component</p>'
});

** 지역 컴포넌트 등록을 위한 todo-list 태그 추가 **

var cmp = {
	template: '<p>This is another local child component333</p>'
};

var app = new Vue({
  el: '#app',
  data: {
    message : 'This is a parent component'
  },
   components: {
    'todo-list': cmp
     }
});


** sibling-component 를 이름으로 갖는 새로운 컴포트 등록 **
options : template, props
[app.js file]
Vue.component('sibling-component', {
  props: ['propsdata'],
  template: '<p>{{ propsdata }}</p>'
});

var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue! passed from Parent Component',
    anotherMessage: 'Hello Vue.js! passed from Parent Component'
  }
});

<!-- sibling-component 등록 -->
[index.html file]
<sibling-component v-bind:propsdata="anotherMessage"></sibling-component>


** /login' url을 추가하고, LoginHeader, LoginBody, LoginFooter 컴포넌트를 추가 **


<div id="app">
  <router-view name="header"></router-view>
  <router-view></router-view>
  <router-view name="footer"></router-view>
</div>


<script>
  var LoginBody = { template: '<div>This is LoginBody</div>' };
  var LoginHeader = { template: '<div>This is LoginHeader</div>' };
  var LoginFooter = { template: '<div>This is LoginFooter</div>' };

  var router = new VueRouter({
    routes: [
      // 실습 #1 - '/login' url을 추가하고, LoginHeader, LoginBody, LoginFooter 컴포넌트를 추가
      {
        path: '/login',
        components: {
          default: LoginBody,
          header: LoginHeader,
          footer: LoginFooter
        }
      },
    ]
  })

  var app = new Vue({
    router
  }).$mount('#app');

</script>



** 머스타쉬 태그  데이터바인딩 ** 
[index.html file]

<div id="app">
      <header>
        <h3>
          <!-- #1. 데이터 속성  추가 -->
          {{ message }}, {{ secondMessage }}
        </h3>
      </header>
      <section>
        <!-- #2. uid 값을 변경한 후 크롬 개발자 도구의 '요소 검사' 기능으로 아래 p 태그의 id 값 확인 -->
        <p v-bind:id="uid"></p>
        <button v-on:click="clickBtn">alert</button>
        <!-- 위 코드와 아래 코드는 동일한 역할을 수행. v-on:를 간소화한 문법은 @ -->
        <!-- <button @click="clickBtn">alert</button> -->
        <!-- #3. button 태그를 추가하고 새로 추가한 클릭 메서드를 연결 -->
        <button v-on:click="clickBtn2">button 2</button>
        <!-- #4. 데이터의 flag 속성 flag 값의따라 화면노출-->
        <ul v-if="flag">
          <li>1</li>
          <li>2</li>
          <li>3</li>
        </ul>
      </section>
    </div>


[app.js file]

var app = new Vue({
  el: '#app',
  data: {
    message : 'Hello Vue.js',
    // #1 새로운 데이터 속성을 1개 추가하고, 머스타쉬 {{ }} 데이터 바인딩
     secondMessage : 'with Do it! Easys Publishing',

    uid: '30',
    // #2  uid를 크롬 개발자 도구의 '화면 요소 검사 기능' 으로 보면 30으로 보여짐

    flag: true
    // #4 위 flag 값을 false로 변경했을 때 화면에 비노출
  },

  //경고창 버튼을 클릭했을때 해당 이벤트를 감지하여 methods 속성에 선언한 popupAlert() 메서드를 수행합니다. 결과적으로 브라우저 기본 경고창을 엽니다.
  methods: {
    // ES6 문법
    clickBtn() {
      console.log("hi");
    },
    // ES5 문법 - 위 ES6 문법과 동일한 코드
    // clickBtn: function() {
    //   console.log("hi");
    // }
  }
});



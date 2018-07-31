<template>
	<div class="home_h">
		 <header class="m_header">
                <div class="m_header_box" id="my_search">
                    <a href="#" @click="goIndex" class="icon_logo"></a>
                    <form action="#">
                        <span class="icon_search" @click="goSearch($event)"></span>
                        <input type="search" ref="search" @focus="goSearch($event)" class="search" placeholder="点击搜索">
                    </form>
                    <router-link :to="userDo.path" v-show="userDo.path" class="logo_btn">{{ userDo.text }}</router-link>
                    <span @click="logout" v-show="!userDo.path" class="logo_btn">{{ userDo.text }}</span>
                </div>
            </header>
	</div>
</template>
<script>
export default {
  data() {
    return {
      userDo: {
        user: "",
        text: "登陆",
        path: "/login"
      }
    };
  },
  methods: {
    async goSearch(event) {
      try {
        const _this = this;
        this.$router.push("/search");
        let val = this.$refs.search.value;
        const result = await _this.$http.get("/search", {
          params: {
            kw: val
          }
        });
        console.log(data);
        this.$router.push("/search");
      } catch (err) {
        console.log(err);
      }

      // this.axios.get('/search',(data)=>{
      //     console.log(data);
      // })
      // window.event? window.event.returnValue = false : event.preventDefault();
    },
    async getUserInfo() {
      const _this = this;
      const session = window.sessionStorage;
      let userObj = {};
      try {
        if (session.getItem("userInfo")) {
          let uObj = JSON.parse(session.userInfo);
          let { user_id } = uObj;
          const res = await _this.$http.get("/userinfo", {
            params: {
              uId: user_id
            }
          });
          if (res.data) {
            userObj = res.data;
            _this.userDo.user = userObj.user_name;
            _this.userDo.text = "退出";
            _this.userDo.path = "";
            console.log("userObj:" + _this.userObj);
          }
        }
      } catch (error) {
        conosle.log(error);
      }
    },
    logout() {
      const userInfo = sessionStorage.getItem("userInfo");
      if (!this.userDo.path && userInfo) {
        console.log("logout");
        sessionStorage.removeItem("userInfo");
        this.initData();
        this.getUserInfo();
        // setTimeout(() => {
        //   this.$router.push("/login");
        // }, 300);
      }
    },
    initData() {
      this.userDo = {
        user: "",
        text: "登陆",
        path: "/login"
      };
    },
    goIndex() {
      this.$router.push("/");
    }
  },
  mounted() {
      this.initData();
    this.getUserInfo();
  }
};
</script>
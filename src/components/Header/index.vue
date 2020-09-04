<template>
<div>
    <van-nav-bar :title="title" 
     left-text="返回" 
     right-text=登出
     left-arrow
     @click-right="loginOut"
     @click-left="goBack"
    v-show="showHeader"/>
    
</div>
     
</template>
<script>
import { NavBar } from 'vant';
import { mapState } from 'vuex';
import { removeLocalStorage } from '@/utils/local-storage';
import { authInfo, authLogout, authProfile } from '@/api/api';
export default {
    name:"v-header",
    data(){
        return {
            title:"",
        };
    },
    computed: {
        showHeader:function(){
            let header=this.$store.getters.showHeader;
            this.title=this.$store.getters.titleHeader;
            return header
        }
    },
    methods: {
        goBack() {
            this.$router.back(-1);
        },
         loginOut() {
            authLogout().then(res => {
            removeLocalStorage('Authorization')
            removeLocalStorage('avatar')
            removeLocalStorage('nickName')
            this.$router.push({ name: 'home' });
            });
        }
   },
   components: {
    [NavBar.name]:NavBar,
  }
}
</script>

<template>
        <div class="bl"></div>
        <div id="in" class="bt">欢迎登陆</div>
        <div id="in"><input type="text" id="put"  placeholder="请输入用户名" v-model="uname"></div>
        <div id="in"><input type="text" id="put" placeholder="请输入密码" v-model="passwd"></div>
        <div id="in"><button @click="login">{{ login_btn }}</button>
             <button @click="register">{{ register_btn}}</button>
        </div>
    </template>
    
    <script setup lang="ts">
    import axios from 'axios'
    import { ref } from 'vue'
    import { useRouter } from 'vue-router'
    import { uname,passwd, serverIp} from '../../config.js';
    
        const router = useRouter() // 在 setup 中获取 router 实例
        const login_btn = ref('登录')
        const register_btn =  ref('注册')
    
        const login =()=>{
          login_btn.value='登陆中'
          axios.get(serverIp+'/login',{
            params:{
                username: uname.value,
                password: passwd.value
            }
          }
         ).then((res) => {
          alert(res.data)
          login_btn.value='登录'
          if(res.data=='login success'){
            router.push('/filetd')
          }          
        }).catch((err) => {
          alert(err)
          login_btn.value='登录'
        })
        }
        const register =()=>{
          register_btn.value='注册中'
          router.push('/register')
        }

    </script>
    
    <style>
    .bl{
      height: 40px;
      text-align: center;
    }
    .bt{
      font-size: 20px;
      line-height: 1.5;
      color:rgb(208, 176, 205);
    }
    #in{
      text-align: center;
      margin: 10px 5px 0px 0px;
    }
    
    #put{
      border: 1px solid #b79d75;
      border-radius: 5px;
      
    }
    button {
      margin: 0px 10px 10px 0px;
      background-color: rgb(231, 228, 210);
      border-radius: 8px;
      border: 1px solid #f4f2ef;
    }
    </style>
    
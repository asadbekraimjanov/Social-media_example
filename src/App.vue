<template>
 <div>
   <el-header class="d-flex align-items-center flex-nowrap main-header" >
     <img class="header-logo" src="./components/images/istockphoto-1201523214-612x612.jpg" alt="logo.png">
     <a href="el-divider">Turagram</a>
     <el-tabs v-model="activeName" class="demo-tabs" @tab-click="handleClick">
       <el-tab-pane label="Home" name="first"></el-tab-pane>
       <el-tab-pane label="Likes" name="second"></el-tab-pane>
       <el-tab-pane label="Profile" name="third"></el-tab-pane>
       <el-tab-pane label="Users" name="fourth"></el-tab-pane>
     </el-tabs>
     <div class="main-header-buttons">
       <el-button class="el-button" @click="clickLike"><el-icon><i class="fa-regular fa-heart"/></el-icon></el-button>
       <el-button class="el-button" @click="clickUser"><i class="fa-regular fa-user"></i></el-button>
       <el-button class="el-button"><i class="fa-regular fa-comment"></i></el-button>
     </div>
     <el-avatar class="el-avatar" src="../src/components/images/avatar2.jpg"></el-avatar>
   </el-header>
   <el-divider id="el-divider" class="el-divider"></el-divider>
   <el-scrollbar height="100vh">
     <el-main class="el-main">
       <app-likes :clickUser="clickUser"  :comments="comments" :users="users" v-if="changeMenu == 6"></app-likes>
       <app-home v-for="(item, numb) in 5" :users="users"
                 :numb="numb" :comments="comments" :photos="photos"
                 v-if="changeMenu != 6 && changeMenu != 7 && changeMenu != 8"
       ></app-home>
       <app-profile :photos="photos" :comments="comments" v-if="changeMenu != 6 && changeMenu != 5 && changeMenu != 8"></app-profile>
       <app-users v-if="changeMenu != 6 && changeMenu != 5 && changeMenu != 7"></app-users>
     </el-main>
     <el-footer>
       <div class="footer-container container">
         <ul class="d-flex justify-content-around">
           <li><a>About us</a></li>
           <li><a>Support</a></li>
           <li><a>Press</a></li>
           <li><a>API</a></li>
           <li><a>Jobs</a></li>
         </ul>
         <ul class="d-flex justify-content-around">
           <li><a>Privacy</a></li>
           <li><a>Terms</a></li>
         </ul>
         <ul class="d-flex justify-content-center">
           <li><a href="https://instagram.com"><i class="fa-brands fa-square-instagram"></i></a></li>
           <li><a href="https://twitter.com"><i class="fa-brands fa-twitter"></i></a></li>
           <li><a href="https://facebook.com"><i class="fa-brands fa-facebook-f"></i></a></li>
         </ul>
         <ul class="d-flex justify-content-center mt-4 mb-4 fs-6"><li>created by @asadbekraimjonov09</li></ul>
       </div>
     </el-footer>
   </el-scrollbar>
 </div>
</template>

<script>
import axios from "axios";
import AppHome from './components/AppHome.vue';
import AppLikes from "@/components/AppLikes.vue";
import AppHomeComments from "@/components/AppHomeComments.vue";
import AppProfile from './components/AppProfile.vue';
import test from './components/test.vue';

export default {
  data(){
    return{
      changeMenu: 5,
      activeName: 'first',
      photos: [],
      comments: [],
      users: [],
    }
  },
  methods: {
    handleClick(tab){
      this.changeMenu = tab.uid
    },
    clickUser(){
      this.activeName = 'third'
      this.changeMenu = 7
    },
    clickLike(){
      this.activeName = 'second'
      this.changeMenu = 6
    },
    getUsers(){
      axios.get('https://jsonplaceholder.typicode.com/users')
          .then(rest => {
            this.users = rest.data
          }).catch(error => console.log(error))
    },
    getPhotos(){
      axios.get('https://jsonplaceholder.typicode.com/photos')
          .then(rest => {
            this.photos = rest.data
          }).catch(error => console.log(error))
    },
    getComments(){
      axios.get('https://jsonplaceholder.typicode.com/comments')
          .then(rest => {
            this.comments = rest.data
          }).catch(error => console.log(error))
    },
    openDrawer() {
      this.drawer = !this.drawer
      console.log(this.drawer)
    }
  },
  mounted(){
    this.getPhotos()
    this.getComments()
    this.getUsers()
    console.log('Drawer data', this.drawer)
  },

  components: {
    AppHomeComments,
    'app-home': AppHome,
    'app-likes': AppLikes,
    'app-profile': AppProfile,
    'app-users': test
  }
}
</script>

<style>
.footer-container ul:nth-child(2){
  margin-top: 50px;
}
.footer-container ul:nth-child(3){
  margin-top: 50px;
}
.footer-container ul:nth-child(3) li{
  font-size: 24px;
  margin: 0 10px;
}
.footer-container ul li a{
  color: #637587;
}
.footer-container ul li{
  font-family: Plus Jakarta Sans;
  font-size: 16px;
  font-weight: 400;
  line-height: 24px;
  letter-spacing: 0px;
  text-decoration: none;
  color: #637587;
  cursor: pointer;
}
.footer-container ul li:hover{
  text-decoration: underline;
}
.footer-container{
  width: 100%;
}
.footer-container ul{
  width: 100%;
  list-style-type: none;
}
.el-tabs__item.is-top{
  translate: 0 -13px;
}
.el-tabs{
  margin-top: 40px;
  margin-left: 50%;
  z-index: 10;
}
.el-tabs__item{
  font-family: Plus Jakarta Sans;
  font-size: 18px;
  font-weight: 500;
  line-height: 21px;
  letter-spacing: 0px;
  text-align: left;
  color: #121417;
}
.main-header{
  position: fixed;
  width: 100%;
  height: 65px;
  top: 0;
  background-color: #ffffff;
  z-index: 100;
}
.header-logo{
  display: inline-block;
  height: 50px;
  margin-left: 3%;
}
.header-logo:hover{
  color: var(--el-color-primary);
}
.main-header a{
  font-family: Plus Jakarta Sans;
  font-size: 18px;
  font-weight: 900;
  line-height: 23px;
  letter-spacing: -0.27000001072883606px;
  text-align: left;
  text-decoration: none;
  color: #121417;
}
.main-header a:hover{
  color: var(--el-color-primary);
  cursor: pointer;
}
.el-divider{
  margin-top: 65px;
  position: fixed;
  z-index: 100;
}
.main-header-buttons{
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: nowrap;
  margin-left: 5%;
}
.main-header-buttons .el-button{
  height: 40px;
  width: 40px;
  background-color: #F0F2F5;
  border: none;
  border-radius: 10px;
  font-size: 20px;
}
.el-avatar{
 margin-left: 2%;
}
.container{
  margin-top: 70px;
}
.main-info{
  margin-top: 50px;
  width: 100%;
  margin-left: 5%;
}
.main-info h1{
  font-family: Plus Jakarta Sans;
  font-size: 4em;
  font-weight: 800;
  line-height: 60px;
  letter-spacing: -1.5839999914169312px;
  text-align: left;
  color: #121417;
}
.main-info p{
  font-family: Plus Jakarta Sans;
  margin-top: 20px;
  font-size: 16px;
  font-weight: 400;
  line-height: 24px;
  letter-spacing: 0px;
  text-align: left;
  color: #121417;
}
.el-main-image{
  width: 90%;
  height: 322px;
  margin-left: 5%;
  margin-top: 50px;
  border-radius: 10px;
}
.view-comment-btn{
  padding: 0 20px 0 20px;
  width: 170px;
  height: 50px;
  font-family: Plus Jakarta Sans;
  font-size: 16px;
  font-weight: 700;
  line-height: 24px;
  letter-spacing: 0.23999999463558197px;
  border-radius: 15px;
  background-color: var(--el-color-primary-dark-2);
  margin-top: 30px;
}
</style>

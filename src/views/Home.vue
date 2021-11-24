<template>
  <div>
     <div class="main-container">
          <h1 style="font-family:'Roboto', sans-serif; color:#130f40">Devfinder</h1>
          <form class="search-box" >
            <input class="search-text" type="text" name="Search User" placeholder="Search User" v-model="username">
            <button class="search-btn" type="button" @click="getUserInfo"><i class="fas fa-search"></i></button>
          </form>
          <UserInfo :userInfo="userInfo"  />
      </div>
  </div>
</template>

<script>
import UserInfo from "../components/UserInfo.vue";
import {ref} from "vue"; 
import axios from "axios";
export default {
  name: 'Home',
  components: { UserInfo },

  setup() {
    const username = ref("");
    const userInfo =  ref(null);

    const getUserInfo = async () => {
      try {
        const response = await axios.get(`https://api.github.com/users/${username.value}`);
        const result = response.data;
        console.log(result);
        userInfo.value = {
          image:result.avatar_url,
          name: result.name,
          user_name: result.username,
          joined: result.created_at,
          bio: result.bio,
          repos: result.public_repos,
          followers: result.followers,
          following: result.following,
          location: result.location,
          twitter: result.twitter_username,
          blog:result.blog,
          company: result.company
        }
        
      } catch (error) {
        alert(error.message);
      }
    };
    return {
      username,
      userInfo,
      getUserInfo
    }
  }
}
</script>

<style scoped>
  

  .main-container{
    margin: 50px auto;
    padding:45px;
    width: 700px;
    height:300px;
    color: black;
  }

  h4{
    font-family: 'Roboto', sans-serif;
  }

  .search-box{
    background: #30336b;
    height: 30px;
    border-radius: 40px;
    padding: 10px;
    width:600px;
  }

  .search-btn{
    color: #535c68;
    float: right;
    width:27px;
    height: 27px;
    border-radius: 50%;
    background: white;
    display: flex;
    justify-content: center;
    align-items: center;
    transition: 0.4s;
    cursor: pointer;
    border: none;
  }

  .search-btn:hover{
    color:  white;
    background: #30336b;
  }

  .search-text{
    border: none;
    background: none;
    outline: none;
    float: left;
    padding: 0;
    color: white;
    font-size: 16px;
    transition: 0.4s;
    line-height: 28px;
    padding: 0, 6px;
  }

  .search-text::placeholder{
    color:#535c68;
  }

</style>


<style>

</style>
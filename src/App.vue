<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>

  <header>
    <div class="container">
        <RouterLink to="/" class="logo">
            <h1>Find<br>Band<br>Member</h1>
        </RouterLink>
        <label for="switch"><img src="./assets/hamburger.png"></label>
        <div class="navbar">
          <input type="checkbox" id="switch">
            <ul class="menu">
                <!-- <li>
                    <a href="#">練團室地圖</a>
                </li> -->
                <li>
                  <RouterLink to="/" class="info_btn">Home</RouterLink>
                </li>
                <li>
                  <RouterLink to="/information" class="info_btn">留言版</RouterLink>
                </li>
                <li>
                  <RouterLink to="/login" class="login_btn">登入/註冊</RouterLink>
                </li>
            </ul>
        </div>
    </div>
  </header>

  <RouterView />

</template>

<style lang="scss" scoped>

.container {
  background: #2f2f2f;
  box-shadow: 0px 1px 3px #00000088;
  overflow: hidden;
  &::after {
    content: "";
    display: block;
    clear: both;
  }
  .logo {
    float: left;
    padding-left: 50px;
    text-decoration: none;
    color: #D1603D;
    font-size: 20px;
    font-weight: bold;
    cursor: pointer;
    margin: 0 50px;
    margin: 10px 0;
    &:hover {
      color: #fff;
    }
  }
}
.navbar input {
  display: none;
}

.container label {
  float: right;
  padding-right: 50px;
  line-height: 50px;
  cursor: pointer;
  img {
    width: 38px;   
    margin-top: 20px;
    vertical-align: middle;
  }
}
.menu {
  clear: both;
  background: #fff;
  color: #D1603D;
  li {
    text-align: center;
    border-bottom: 1px solid #3a3a3a;
    a {
      display: block;
      line-height: 50px;
      font-size: 18px;
      color: #D1603D;
      text-decoration: none;
      &:hover {
        color: #fff;
      }
    }
  }
}
.menu {
  background: #2f2f2f;
  max-height: 0;
  overflow: hidden;
  transition: .2s;
}

input:checked ~ .menu {
  max-height: 300px;
}


@media screen and (min-width: 768px) {
  label {
    display: none;
  }
  .menu {
    float: right;
    clear: none;
    max-height: 50px;
    background: #2f2f2f;
    margin-top: 16px;
    
    li {
      display: inline-block;
      a {
        padding: 0 15px;  
        color: #D1603D;
      }
    }
  }
}


    /* .container {
        background-color: #2f2f2f;
        height: 80px;
        max-width: 100vh;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .container a {
        text-decoration: none;
        color: #D1603D;
        font-size: large;
        font-weight: bold;
        cursor: pointer;
        margin: 0 50px;
    }

    .container .logo {
      font-size: 24px;
    }
    .container a:hover {
        color: #fff;
    }

    .navbar ul {
        width: 600px;
        display: flex;
        justify-content: space-around;
        align-items: center;
    } */

</style>
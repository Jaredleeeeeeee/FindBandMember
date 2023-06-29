<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>

  <header>
    <div class="container">
        <RouterLink to="/" class="logo">
            <h1>Find<br>Band<br>Member</h1>
        </RouterLink>
        <div class="navbar">
            <ul>
                <!-- <li>
                    <a href="#">練團室地圖</a>
                </li> -->
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

<style scoped>
    .container {
        background-color: #2f2f2f;
        height: 80px;
        max-width: 100%;
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
        width: 400px;
        display: flex;
        justify-content: space-around;
        align-items: center;
    }
</style>

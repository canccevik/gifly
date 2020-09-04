<template>
  <div>
    <div class="header">
      <div class="header-content">
        <router-link to="/"><span class="title">GIFLY</span></router-link>
        <router-link to="/search">🔎</router-link>
      </div>
    </div>

    <div class="content">
      <router-view />
    </div>

    <div class="footer">
      <p>Made with ❤️ by <a href="https://github.com/canccevik" target="blank" class="link">Can Çevik</a>.</p>
    </div>
  </div>
</template>

<style>
  @import url('https://fonts.googleapis.com/css2?family=Poppins&display=swap');

  * {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: 'Poppins';
  }

  ::-webkit-scrollbar {
    background: black;
    transition: .5s;
  }

  ::-webkit-scrollbar-thumb {
    background: white;
      border: 2px solid black;
      transition: .5s;
  }

  ::-webkit-scrollbar-thumb:hover {
      background: black;
  }

  ::-webkit-scrollbar:hover {
    background: white;
  }

  .header {
    padding: 5px 0;
    background-color: black;
    text-align: center;
    color: white;
  }

  .header-content {
    width: 70%;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .header-content a {
    text-decoration: none;
    font-size: 30px;
  }

  .header .title {
    font-size: 40px;
    letter-spacing: 3px;
    text-decoration: none;
    color: white;
    font-weight: bold;
  }

  .content {
    width: 70%;
    margin: 0 auto;
    margin-top: 20px;
  }

  .footer {
    width: 100%;
    padding: 10px 0;
    margin-top: 20px;
    text-align: center;
    background-color: black;
    color: white;
  }

  .link {
    color: white;
    text-decoration: none;
  }

  .link:hover {
    transition: .2s;
    text-decoration: underline;
  }

  @media only screen and (max-width: 767px) {
    .content {
      width: 95%;
    }

    .header-content {
      width: 90%;
    }
  }
</style>
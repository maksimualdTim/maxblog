<template>
  <div class="wrapper">
      <header class="header">
        <div class="container">
          <div class="header__main">
            <router-link to="/">
              <img src="@/assets/logo.png" alt="logo">
            </router-link>
            <div class="add">
              <a href="#">
                <img src="@/assets/header_main.png" alt="add">
              </a>
            </div>
          </div>
          <div class="header__menu">
            <ul class="header__menu-list">
              <li class="header__menu-item">
                <router-link class="header__menu-link" to="/">Home</router-link>
              </li>
              <li class="header__menu-item">
                <router-link to="/about" class="header__menu-link">About</router-link>
              </li>
              <li class="header__menu-item">
                <router-link to="/news" class="header__menu-link">News</router-link>
              </li>
            </ul>
            <div class="header__menu-right">
              <div class="search__wrapper">
                <a href="#" class="search">
                  <i class="fa fa-search"></i>
                </a>
              </div>
              <div class="login__wrapper">
                <a href="#" class="login">
                  <i class="fas fa-user"></i>
                </a>
              </div>
            </div>
          </div>
        </div>
      </header>
      <div class="brekignews"></div>
      <router-view></router-view>
      <footer class="footer">
        <div class="container">
          <div class="footer__top">
            <div class="col-md-4 footer__card">
              <h3 class="footer__card-title">About Us</h3>
              <div class="footer__logo">
                <img src="@/assets/footer_logo.png" alt="footer_logo">
              </div>
              <div class="footer__desc">
                <p>Lorem ipsum dolor sit amet consectetur adipiscing elit.
                  Donec pretium est quis sem fermentum malesuada tellus feugiat.
                  Nunc libero mi mollis quis luctus posuere quis luctus
                  libero quis consectetur</p>
              </div>
              <div class="footer__tags">
                <div class="footer__card-title">Tags</div>
                <ul class="footer__tags-list">
                  <li class="footer__tag">
                    <a href="#" class="footer__tag-link fas fa-tags">bike</a>
                  </li>
                  <li class="footer__tag">
                    <a href="#" class="footer__tag-link fas fa-tags">car</a>
                  </li>
                  <li class="footer__tag">
                    <a href="#" class="footer__tag-link fas fa-tags">city</a>
                  </li>
                  <li class="footer__tag">
                    <a href="#" class="footer__tag-link fas fa-tags">featured</a>
                  </li>
                  <li class="footer__tag">
                    <a href="#" class="footer__tag-link fas fa-tags">field</a>
                  </li>
                  <li class="footer__tag">
                    <a href="#" class="footer__tag-link fas fa-tags">gallery</a>
                  </li>
                  <li class="footer__tag">
                    <a href="#" class="footer__tag-link fas fa-tags">nature</a>
                  </li>
                  <li class="footer__tag">
                    <a href="#" class="footer__tag-link fas fa-tags">sea</a>
                  </li>
                  <li class="footer__tag">
                    <a href="#" class="footer__tag-link fas fa-tags">sheep</a>
                  </li>
                  <li class="footer__tag">
                    <a href="#" class="footer__tag-link fas fa-tags">street</a>
                  </li>
                  <li class="footer__tag">
                    <a href="#" class="footer__tag-link fas fa-tags">video</a>
                  </li>
                </ul>
              </div>
            </div>
            <div class="col-md-4 footer__card">
              <h3 class="footer__card-title">Latest Posts</h3>
              <div class="footer__posts">
                <div class="footer__post" v-for="footer_post in footer_posts" :key="footer_post.id">
                  <div class="footer__post-preview">
                    <a href="#" class="footer__post-linkimg">
                      <img src="https://demo.themeruby.com/maxblog/wp-content/uploads/2015/03/829-90x63.jpg">
                    </a>
                  </div>
                  <div class="footer__post-content">
                    <h3 class="footer__post-title">
                      <router-link :to="{path: '/articles/' + footer_post.id, params: footer_post}">{{footer_post.title}}</router-link>
                    </h3>
                    <div class="footer__post-subtitle">
                      <div class="footer__post-category">
                        <router-link :to="{path: '/articles/category/'+footer_post.category.name}">{{footer_post.category.name}}</router-link>
                      </div>
                      <div class="footer__post-date">{{footer_post.created_at}}</div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="col-md-4 footer__card">
              <h3 class="footer__card-title">My photo Stream</h3>
              <div class="footer__photos"></div>
            </div>
          </div>
        </div>
        <div class="footer__bottom">
          <div class="container">
            <div class="copyright">
              Copyright © 2021 Theme-Ruby. Powered by Maksimuald
            </div>
          </div>
        </div>
      </footer>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',

  data(){
    return {
      footer_posts: '',
      footer_posts_count: 4,
    }
  },
  methods:{
    async getFooterPosts(count){
      const res = await axios.get('http://localhost:8080/api/articles?last=' + count);
      this.footer_posts = res.data;
    }
  },
  created() {
    this.getFooterPosts(this.footer_posts_count);
  },
};
</script>
<style lang="scss">
@import "assets/styles/variables.scss";

.header{
  &__main{
    padding: 20px 0;
    margin: 0 30px;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  &__menu{
    background: $menu;
    display: flex;
    justify-content: space-between;
  }
  &__menu-list{
    display: flex;
    align-items: center;
    align-content: center;
  }
  &__menu-item{
    height: 48px;
    transition-duration: 0.3s;

    &:hover{
      background: $main-color;
      transition-duration: 0.3s;
    }
  }
  &__menu-link{
    color: $menu-link;
    text-decoration: none;
    padding: 0 21px;
    display: block;
    line-height: 48px;
    text-transform: uppercase;
  }
  &__menu-right{
    display: flex;
  }
}

.login,
.search{
  padding: 0 21px;
  display: block;
  transition-duration: .5s;
  line-height: 48px;
  &:hover{
    transition-duration: .5s;
    background: $main-color;
  }
}
.search i:before,
.login i:before{
  color: $menu-link;
}
.footer{
  color:$menu-link;
  background: #212728;
  &__top{
    padding: 45px 15px 15px;
    display: flex;
  }
  &__card{
    padding: 0 15px;
  }
  &__bottom{
    background: $menu;
  }
  &__card-title{
    border-bottom: 1px solid rgba(0,0,0,.08);
    text-transform: uppercase;
    margin: 0 15px 25px;
    &:before{
      content: '';
      display: inline-block;
      width: 10px;
      height: 10px;
      position: relative;
      margin-right: 12px;
      opacity: .2;
      background: #fff;
    }
  }
  &__desc{
    margin-top: 25px;
    margin-bottom: 30px;
  }
  &__desc p{
    font-size: 12px;
    opacity: .8;
    line-height: 1.6em;
    font-weight: 400;
  }
  &__tags{

  }
  &__tags-list{
    display: flex;
    flex-wrap: wrap;
  }
  &__tag{
    margin-right: 7px;
    margin-bottom: 7px;
  }
  &__tag-link:before{
    margin-right: 5px;
  }
  &__tag-link{
    text-transform: lowercase !important;
    display: block;
    color: $menu-link;
    border: 1px solid $menu-link;
    padding: 4px 7px;
    text-decoration: none;
    transition-duration: .5s;

  }
  &__tag-link:hover{
    color: #fff;
    border: 1px solid #fff;
    text-decoration: underline;
    transition-duration: .5s;
  }
  &__post{
    display: flex;
    padding: 10px 0;
  }
  &__post-subtitle{
    display: flex;
  }
  &__post-preview{
    margin-right: 15px;
  }
  &__post-title{
    margin-bottom: 10px;
  }
  &__post-title a{
    color: $menu-link;
    text-decoration: none;
  }
  &__post-title a:hover{
    text-decoration: underline;
  }
  &__post-category a{
    color: $menu-link;
    opacity: .8;
    transition-duration: .5s;
  }
  &__post-category a:hover{
    color: $main-color;
    opacity: .8;
    transition-duration: .5s;
  }
  &__post-category:after{
    content: '/';
    margin: 0 5px;
  }
  &__post-date{
    font-size: 12px;
    opacity: .8;
  }
}
.copyright{
  text-align: center;
  font-size: .9em;
  padding: 15px 30px;
}



</style>

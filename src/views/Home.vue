<template>

  <div class="container">
    <v-app>
      <v-carousel
          cycle
          height="400"
          hide-delimiter-background
          show-arrows-on-hover
      >
        <template v-slot:prev="{ on, attrs }">
          <v-btn
              color="success"
              v-bind="attrs"
              v-on="on"
          >Previous slide</v-btn>
        </template>
        <template v-slot:next="{ on, attrs }">
          <v-btn
              color="info"
              v-bind="attrs"
              v-on="on"
          >Next slide</v-btn>
        </template>
        <v-carousel-item
            v-for="(carousel_post, i) in carousel_posts"
            :key="i"
            class="carousel__item"
        >
            <v-sheet
                :color="colors[i]"
                height="100%"
            >
              <router-link  :to="{path: '/articles/'+ carousel_post.id}" class="carousel__item-link">
                <v-row
                    align="center"
                    justify="center"
                    class="fill-height carousel__row-top"
                >
                  <div class="carousel__content">
                    <div class="text-h2 carousel__title">
                      {{ carousel_post.title}}
                    </div>
                    <div class="carousel__subtitle">
                      <div class="carousel__post-category carousel__post">
                        <router-link class="carousel__post-link" :to="{path: '/articles/?category_id=' + carousel_post.category_id}">{{carousel_post.category.name}}</router-link>
                      </div>
                      <div class="carousel__post-date carousel__post">{{carousel_post.created_at}}</div>
                      <div class="carousel__title-comments carousel__post">comments</div>
                    </div>
                  </div>
                </v-row>
              </router-link>
            </v-sheet>
        </v-carousel-item>
      </v-carousel>

      <main class="main">
        <div class="posts" v-for="(category, index) in postsFromAllCategories" :key="index" >
          <div class="posts__item-category">
            <router-link  class="posts__item-link" :to="{path: '/articles/?category_id=' + category[category_number].category_id}">{{index}}</router-link>
          </div>
          <div class="posts__item" v-for="(post, index) in category" :key="index">
            <div class="posts__item-content">
              <div v-if="index === 1" class="posts__item-left">
                <div class="posts__item-img">
                  <router-link :to="{path: '/articles/'}"></router-link>
                </div>
                <div class="posts__item-tags">
                  <div class="posts__item-category">
                    <router-link :to="{path: '/articles/?category_id' + post.category_id}">{{post.category.name}}</router-link>
                  </div>
                  <div class="posts__item-date">{{post.created_at}}</div>
                </div>
                <div class="posts__item-desc"></div>
              </div>
              <div v-else class="posts__item-right">
                <div class="posts__item-title">
                  <router-link :to="{path: '/articles/' + post.id}">{{post.title}}</router-link>
                </div>
                <div class="posts__item-tags">
                  <div class="posts__item-category">
                    <router-link :to="{path: '/articles/?category_id' + post.category_id}">{{post.category.name}}</router-link>
                  </div>
                  <div class="posts__item-date">{{post.created_at}}</div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </main>

    </v-app>

  </div>
</template>


<script>
import axios from "axios";

export default {
  data () {
    return {
      colors: [
        'indigo',
        'warning',
        'pink darken-2',
        'red lighten-1',
        'deep-purple accent-4',
          'red',
      ],
      slides: [
        'First',
        'Second',
        'Third',
        'Fourth',
        'Fifth',
      ],
      postsFromAllCategories: [],
      categories: [],
      carousel_posts: [],
      category_number: 0,
    }
  },
  methods:{
    async getSliderPosts(count = 6){
      const res = await axios.get('http://localhost:8080/api/articles?last=' + count);
      this.carousel_posts = res.data;
    },
    async getLatestPostsFromAllCategories(count = 6){
      const res = await axios.get('http://localhost:8080/api/articles/all/categories?last=' + count);
      this.categories = Object.keys(res.data);
      this.postsFromAllCategories = res.data;
    },
  },
  created() {
    this.getLatestPostsFromAllCategories();
    this.getSliderPosts();
  },
}
</script>

<style lang="scss">
@import "@/assets/styles/variables.scss";

.carousel__item{
  &-link{
    text-decoration: none;
    color: $menu-link;
  }
  &-link:hover{
    text-decoration: underline;
    text-decoration-color: $menu-link;
  }
}
.carousel__post{
  color: $menu-link;
  margin: 0 auto;
  &-category{
    font-family: Roboto, sans-serif;
    font-weight: 400;
    text-transform: uppercase;
    font-size: 10px;
  }
}
.carousel__title{
  color: $menu-link;
  font-size: 3em;
  line-height: 1.1em;
}
.carousel__subtitle{
  display: flex;
  margin: 15px 0;
  align-items: center;
}
.carousel__post-link{
  color: $menu-link !important;
  transition-duration: .3s;
  :hover{
    text-decoration: none;
    color: $main-color !important;
    transition-duration: .3s;
  }
}
.main{
  margin-top: 45px;
}
.posts{
  margin-bottom: 30px;
}
.posts__item-category{
  display: block;
  border-bottom: 1px solid #e2e2e2;
  height: 30px;
  margin: 0 15px 25px;
}
.posts__item-link{
  color: $title !important;
  text-decoration: none;
  transition-duration: .3s;
  text-transform: uppercase;
  &:hover{
    color: $main-color !important;
    transition-duration: .3s;
  }
}
</style>

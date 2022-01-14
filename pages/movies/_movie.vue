<template>
  <div class="container detail-container">
      <nuxt-link class="button" to="/">Geri</nuxt-link>
      <div class="detail">
      <div class="img">
         <img :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`" alt="">
      </div>
      <div class="detail-info">
          <div class="detail-title">{{movie.title}}</div>
           <div class="detail-voteaverage">
           Imbd Puanı: {{movie.vote_average}}
          </div>
          <div class="detail-duration detail-color">
            Süre : {{movie.runtime}} Dakika
          </div>
          <div class="detail-overview detail-color">
            {{movie.overview}}
          </div>
          <div class="detail-release detail-color">
            Yayınlanma Tarihi : {{
              new Date(movie.release_date).toLocaleString('tr',{
                month:'long',
                day:'numeric',
                year:'numeric'
              })
            }}
          </div>
         </div>
      </div>
  </div>
</template>

<script>
import axios from "axios"
export default {
  data(){
    return{
      movie:[]
    }
  },
  async fetch(){
      this.getMovie()
  },
  methods:{
    async getMovie(){
      const data = axios.get(
        `https://api.themoviedb.org/3/movie/${this.$route.params.movie}?api_key=4dd3cec5a523f4417a98e1efffddb641&language=tr`)
      const  result = await data
      this.movie = result.data
      console.log(this.movie)
    }
  }
}
</script>

<style>
.detail-container{
  padding-top: 3rem;
  padding-bottom: 3rem;
}
.detail{
  padding-top: 1rem;
  display: flex;
  align-items: center;
  justify-content: center;
}
.img img{
  border-radius: 15px;
}
.detail-info{
  margin-left: 5rem;
  padding: 6rem;
  color: white;
}
.detail-title{
  font-size: 2rem;
  margin-bottom: .5rem;
}
.detail-voteaverage{
  margin-bottom: .5rem;
}
.detail-duration{
  margin-bottom: .5rem;
}
.detail-overview{
  font-size: 1.2rem;
  margin-bottom: 1rem;
}
.detail-color{
  color: rgba(255, 255, 255, 0.589);
}
</style>
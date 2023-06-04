<script setup>
import { ref,computed, onMounted } from 'vue';


import BlogPost from './components/BlogPost.vue';
import PaginatePost from './components/PaginatePost.vue';
import LoadingSpinner from './components/loadingSpinner.vue'
import ButtonCounter from './components/ButtonCounter.vue';

const posts = ref([
  //{ title: 'post 1', id: '1', body: 'descripcion 1' },
  //{ title: 'post 2', id: '2', body: 'descripcion 2' },
  //{ title: 'post 3', id: '3', body: 'descripcion 3' },
  //{ title: 'post 4', id: '4' },
])

const postXpage = 10
const inicio = ref(0)
const fin = ref(postXpage)
const loading = ref(true)

const favorito = ref('')
const cambiarFavorito = (title) => {
  favorito.value = title
}

const next =() => {
  inicio.value = inicio.value + postXpage;
  fin.value = fin.value + postXpage;
}

const previus =() => {
  inicio.value = inicio.value - postXpage;
  fin.value = fin.value - postXpage;
}

const maxLengthpost = computed(() => posts.value.length)

onMounted(async()=>{
  try {
   const res = await fetch('https://jsonplaceholder.typicode.com/posts')
   posts.value = await res.json()


  } catch (error) {
   console.log(error) 
  }finally{
    setTimeout(()=>{
      loading.value = false
    },2000)
  }
})



//fetch('https://jsonplaceholder.typicode.com/posts')
 // .then((result) => result.json() )
  //.then((data) =>{ posts.value = data;})
  //.catch((error)=> console.log(error))
  //.finally(()=> {
   // setTimeout(()=>{
    //  loading.value = false
    //},2000)
    
  //})

</script>

<template>
  <LoadingSpinner v-if="loading"/>

  <div class="container" v-else>
    <h1>APP</h1>
    <h1>Mi Post Favorito: Post {{favorito}}</h1>


    <PaginatePost 
    @nextPage = "next"
    @previusPage = "previus"
    :inicio = "inicio"
    :fin = "fin"
    :maxLengthpost = "maxLengthpost"
    class="mb-2"/>

    <BlogPost 
    v-for="post in posts.slice(inicio, fin)" 
    :key="post.id" 
    :title="post.title" 
    :id="post.id" 
    :body="post.body"
    :cambiarFavorito="cambiarFavorito"
    class="mb-2"></BlogPost>
  </div>
</template>
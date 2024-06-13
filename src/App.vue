<script setup>
import q from "./data/quizes.json"
import {ref, watch} from "vue"
import Card from "./components/Card.vue"

const quizes = ref(q)
const search=ref("")

watch(search,()=>{  //to update quizes list based on search text->watch the changes constantly and update constantly
quizes.value=q.filter(quiz=>quiz.name.toLowerCase().includes(search.value.toLowerCase()))
})

</script>

<template>
  <div class="container">
    <header>
      <h1>
        Quizzes
      </h1>
      <input type="text" v-model.trim="search" placeholder="Search...">
    </header>
    <div class="options-conatiner">
      <Card v-for="quiz in quizes" :key="quiz.id" :quiz="quiz"/>
      <!-- <div v-for="quiz in quizes" :key="quiz.id" class="card">
        <img :src="quiz.img" alt="quizalt">
        <div class="card-text">
          <h2>{{ quiz.name }}</h2>
          <p>{{ quiz.questions.length }} Questions</p>
        </div>
      </div> -->
    </div>
  </div>
</template>

<style scoped>
.container{
max-width: 1000px;
margin: 0 auto;
}
header{
  margin-bottom: 10px;
  margin-top: 30px;
  display: flex;
  align-items: center;
}
header h1{
  font-weight: bold;
  margin-right: 30px;
}
header input{
  border: none;
  background-color: rgba(128,128,128,0.1);
  padding: 10px;
  border-radius: 5px;
}
.options-comtainer{
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
}
</style>
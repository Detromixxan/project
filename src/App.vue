<template>
  <button 
    @click="addNewFeed"
    class="add-btn">
    Добавить карточку
  </button>
  <button 
  @click="delAllcards"
  class="del-btn">
  Удалить карточку
</button>
<input
  v-model="search"
  placeholder= "Введи номер"
  class="inp-search"
  type="text"
  >
  <div>
      Количетсво карточек:
      <strong>
        {{ counter }}
      </strong>
  </div>
  <div
       v-if="posts.length > 0"
       class="container"
       >
      <div 
        v-for="post of data" 
        :key="post.id"
        class="post">
        <span
          v-bind:title="message"
          class="numberNews"
        >
          <strong>Новость номер</strong> {{ post.numberNews }} 
        </span>
        <img 
        :src="img"
        :title="altImg"
        class="imgNews"
        width="250"
        height="250">
        <div
        class="titleNews"
        ><strong>Название:</strong> {{ post.title }} </div>
        <div
        class="descriptionNews"
        ><strong>Описание:</strong> {{ post.body }} </div>
        <button
        @click="delPostInPosts"
        :key="post.btnId"
        class="post-btn"
      >
        <img 
          :src="delImg"
          :title="delTitleImg"
          class="del-img"
          width="50"
          height="50">
      </button>
      </div>
  </div>
  <div 
    v-else="posts.length === 0"
    class="container-clear"
    >
      Добавьте элементы на старинцу
  </div>
</template>

<script>
export default {
  data () {
    return {
      posts:[],
      message: "Номер карточки товара",
      img: "/img/Тимон.jpg",
      altImg: "Картинка",
      delImg: "/img/delImg.webp",
      delTitleImg: "Картинка удаление",
      search: '',
      counter: 0,
    }
  },
  computed: {
    data(){
      if(this.search){
        return this.posts.filter(e => e.id === Number(this.search))
      }
      return this.posts
    },
  },
  methods :{
    addNewFeed() {
      if(this.posts.length === 10){
        alert("Вы добавили 10 карточек!")
      } else if(this.posts.length === 50){
        alert("Вы добавили 50 карточек!")
      }

      const index = this.posts.length + 1;

      this.posts.push({
        id: index,
        numberNews : index,
        img: this.img,
        title: `JavaScript ${index}`,
        body: 'Описание поста',
        btnId: index
      })

      for(let i = 0; i <= this.posts.length; i++){
        return this.counter++
      }
    },
    delAllcards() {
    this.posts.splice(0, this.posts.length)
    this.counter = 0
    },
  },
}
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container{
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  width: 100%;
  background-color: #b2a8a8;
}

.container-clear{
  background-color: #b2a8a8;
  width: 100%;
  height: 1024px;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  color:hwb(0 26% 72%);
  font-size: 48px
}


.post{
  width: 400px;
  height: 450px;
  border-radius: 30px;
  border: 3px solid black;
  padding: 15px;
  margin-top: 30px ;
  margin-right: 30px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.add-btn{
  width: 150px;
  height: 60px;
  border-radius: 30px;
  border: 1px solid gray;
  font-family: 'Times New Roman', Times, serif;
  font-size: 16px;
  font-weight: bold;
  background-color: gray;
  color: black;
  margin-top: 10px;
  margin-bottom: 10px;
  margin-left: 20px;
}

.add-btn:hover{
  background-color: green;
}

.del-btn{
  width: 150px;
  height: 60px;
  border-radius: 30px;
  border: 1px solid gray;
  font-family: 'Times New Roman', Times, serif;
  font-size: 16px;
  font-weight: bold;
  background-color: red;
  color: black;
  margin-top: 10px;
  margin-bottom: 10px;
  margin-left: 20px;
}

.inp-search{
  width: 150px;
  height: 40px;
  border-radius: 10px;
  border: 1px solid gray;
  font-family: 'Times New Roman', Times, serif;
  font-size: 16px;
  font-weight: bold;
  color: black;
  margin-top: 10px;
  margin-bottom: 10px;
  margin-left: 20px;
  padding: 10px;
}

.numberNews{
  margin-top: 0px;
  margin-bottom: 0px;
  font-family: 'Times New Roman', Times, serif;
  font-size: 16px;
  font-weight: bold;
}

.titleNews{
  margin-top: 20px;
  margin-bottom: 0px;
  font-family: 'Times New Roman', Times, serif;
  font-size: 16px;
  font-weight: bold;
}

.imgNews{
  margin-top:30px;
  margin-bottom: 30px;
  border-radius: 30px ;
  margin-left: auto;
  margin-right: auto;
}

.descriptionNews{
  margin-top: 10px;
  margin-bottom: 0px;
  font-family: 'Times New Roman', Times, serif;
  font-size: 16px;
  font-weight: bold;
}
</style>

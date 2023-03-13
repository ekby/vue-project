<script>
import {getBooks, postBook} from "@/api/api";

export default {
  name: 'HelloWorld',
  data() {
    return {
      msg: 'Vue3 + Django',
      // books list data
      books: [
        {name: 'test', author: 't'},
        {name: 'test2', author: 't2'}
      ],
      // book data in the form
      inputBook: {
        "name": "",
        "author": "",
      }
    }
  },
  methods: {
    loadBooks() {
      getBooks().then(response => {
        this.books = response.data
      })
    }, // load books list when visit the page

    bookSubmit() {
      postBook(this.inputBook.name, this.inputBook.author).then(response => {
        console.log(response)
        this.loadBooks()
      })
    } // add a book to backend when click the button
  },
  created: function () {
    this.loadBooks()
  }
}
</script>

<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

    <!-- show books list -->
    <ul class="table">
      <li v-for="(book, index) in books" :key="index" style="display:block">
        {{ index }}-{{ book.name }}-{{ book.author }}
      </li>
    </ul>

    <!-- form to add a book -->
    <form action="" id="shuru">
      输入书名：<input type="text" placeholder="book name" v-model="inputBook.name"><br>
      输入作者：<input type="text" placeholder="book author" v-model="inputBook.author"><br>
    </form>
    <div id="tianjia">
      <button type="submit" @click="bookSubmit()">添加</button>
    </div>
  </div>
</template>

<style scoped>
#shuru {
  margin: 20px  auto 20px;
  max-width: fit-content;
}

#tianjia {
  margin: auto auto 20px;
  max-width: fit-content;
}

.table {
  margin: 20px auto;
  max-width: fit-content;
}

h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
  text-align: center;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}
</style>

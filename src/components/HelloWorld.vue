<template>
  <div>
      <form @submit="addBook">
          <input type="text" name="title" v-model="title" placeholder="Add Book">
          <button type="submit">Add Book</button>
      </form>
  </div>
</template>

<script>
  export default {
      name: "HelloWorld",
      data () {
          return {
              title: ''
          }
      },
      methods: {
          addBook(e){
              e.preventDefault();
              const newBook = {
                  title: this.title,
                  id: Math.floor(Math.random() * 100)
              };
              if (newBook.title !== ''){
                  this.$emit('add-book-event', newBook);
              }
              this.title = ''
          }
      }

  }
</script>
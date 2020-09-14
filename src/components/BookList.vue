<template>
  <div>
    <h1>{{ title }}</h1>
    <ul>
      <BookItem v-for="book in books" :key="book.title" :book="book" />
      <BookForm @addBook="appendBook" />
    </ul>
  </div>
</template>

<script>
import BookItem from "@/components/BookItem.vue";
import BookForm from "@/components/BookForm.vue";

export default {
  name: "BookList",
  data() {
    return {
      title: "All Books",
      books: [
        { title: "Self-Reliance", author: "Ralph Waldo Emerson" },
        { title: "American Gods", author: "Neil Gaiman" },
        { title: "Amusing Ourselves to Death", author: "Neil Postman" },
        {
          title: "Daring Greatly: How the courage to be vulnerable transforms the way we live, love, parent and lead",
          author: "Brene Brown",
        },
        { title: "Don't make me think", author: "Steve Krug" },
        { title: "DRiVE", author: "Daniel Pink" },
      ],
    };
  },
  methods: {
    appendBook(bookTitle, bookAuthor) {
      this.books.push({ title: bookTitle, author: bookAuthor });
    },
  },
  components: { BookItem, BookForm },
};
</script>

<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
</style>

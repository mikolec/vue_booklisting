<template>
  <div>
    <h1>{{ title }}</h1>
    <input type="text" placeholder="Search Books" v-model="searchInput" />
    <ul>
      <BookItem v-for="book in searchedBooks" :key="book.title" :book="book" />
    </ul>
    <hr />
    <BookForm @addBook="appendBook" />
    <hr />
    <h2>Filtered Books By Ownership</h2>
    <select name="holding" id="holding" v-model="holding">
      <option v-for="(filter, index) in filters" :key="index">{{ filter }}</option>
    </select>
    <ul>
      <BookItem v-for="book in filteredBooks" :key="book.title" :book="book" />
    </ul>
  </div>
</template>

<script>
import _ from "lodash";
import BookItem from "@/components/BookItem.vue";
import BookForm from "@/components/BookForm.vue";

export default {
  name: "BookList",
  data() {
    return {
      title: "All Books",
      books: [
        { title: "Self-Reliance", author: "Ralph Waldo Emerson", finishedReading: false, ownership: "borrowed" },
        { title: "American Gods", author: "Neil Gaiman", finishedReading: false, ownership: "bought" },
        { title: "Amusing Ourselves to Death", author: "Neil Postman", finishedReading: false, ownership: "borrowed" },
        {
          title: "Daring Greatly: How the courage to be vulnerable transforms the way we live, love, parent and lead",
          author: "Brene Brown",
          finishedReading: true,
          ownership: "bought",
        },
        { title: "Don't make me think", author: "Steve Krug", finishedReading: false, ownership: "bought" },
        { title: "DRiVE", author: "Daniel Pink", finishedReading: true, ownership: "borrowed" },
      ],
      filters: ["bought", "borrowed"],
      holding: "bought",
      searchInput: "",
    };
  },
  computed: {
    filteredBooks() {
      return _.filter(this.books, ["ownership", this.holding]);
    },
    searchedBooks() {
      const searchFilter = (book) => {
        return book.title.toLowerCase().match(this.searchInput.toLowerCase());
      };
      return _.filter(this.books, searchFilter);
    },
  },
  methods: {
    appendBook(bookData) {
      this.books.push({
        title: bookData.bookTitle,
        author: bookData.bookAuthor,
        finishedReading: bookData.finishedReading,
        ownership: bookData.ownership,
      });
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

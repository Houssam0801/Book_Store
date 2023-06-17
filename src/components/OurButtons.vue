<template>
  <div>
    <div class="buttons d-flex justify-content-end mt-2 me-3">
      <div class="dropdown">
        <button
          class="btn btn-secondary dropdown-toggle mx-2"
          type="button"
          data-bs-toggle="dropdown"
          aria-expanded="false"
        >
          Sort By
        </button>
        <ul class="dropdown-menu p-1">
          <li @click="sortTitle" class="mylist">Title</li>
          <li><hr class="dropdown-divider" /></li>
          <li @click="sortGenre" class="mylist">Genre</li>
          <li><hr class="dropdown-divider" /></li>
          <li @click="sortAuthor" class="mylist">Author</li>
        </ul>
      </div>
      <div>
        <button @click="toggle = !toggle" type="button" class="btn btn-success">
          Add Book
        </button>
      </div>
    </div>
    <div class="row" v-show="toggle">
      <div id="adding" class="col-9 mx-auto mt-2 p-2">
        <div class="text-start">
          <div>
            <p><label for="title">Title:</label></p>
            <input
              type="text"
              class="d-inline-flex focus-ring focus-ring-primary py-1 px-2 text-decoration-none border rounded-2 w-50"
              v-model="newBook.title"
              required
            />
          </div>

          <div>
            <p><label for="content">Content:</label></p>
            <textarea
              type="text"
              rows="3"
              class="d-inline-flex focus-ring focus-ring-primary py-1 px-2 text-decoration-none border rounded-2 w-50"
              v-model="newBook.content"
              required
            ></textarea>
          </div>

          <div>
            <p><label for="genre">Genre:</label></p>
            <input
              type="text"
              class="d-inline-flex focus-ring focus-ring-primary py-1 px-2 text-decoration-none border rounded-2"
              v-model="newBook.genre"
              required
            />
          </div>

          <div>
            <p><label for="author">Author:</label></p>
            <input
              type="text"
              class="d-inline-flex focus-ring focus-ring-primary py-1 px-2 text-decoration-none border rounded-2"
              v-model="newBook.author"
              required
            />
          </div>
        </div>
        <div class="text-end">
          <button
            class="btn btn-outline-success"
            @click="
              addBook();
              toggle = !toggle;
            "
          >
            Save
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "OurButtons",

  props: ["myBooks"],
  data() {
    return {
      myPropCopy: this.myBooks,
      newBook: {
        title: "",
        genre: "",
        content: "",
        author: "",
        editing: "",
      },
      toggle: false,
      counter: this.myBooks.length,
    };
  },

  methods: {
    addBook() {
      this.counter++;
      if (this.newBook.title != "" && this.newBook.content != "") {
        this.myPropCopy.push({
          id: this.counter,
          title: this.newBook.title,
          genre: this.newBook.genre,
          content: this.newBook.content,
          author: this.newBook.author,
          editing: this.newBook.editing,
        });
        this.newBook.title = "";
        this.newBook.genre = "";
        this.newBook.content = "";
        this.newBook.author = "";
      }
    },
    sortTitle() {
      return this.myPropCopy.sort((a, b) =>
        a.title.toLowerCase() > b.title.toLowerCase() ? 1 : -1
      );
    },
    sortGenre() {
      return this.myPropCopy.sort((a, b) =>
        a.genre.toLowerCase() > b.genre.toLowerCase() ? 1 : -1
      );
    },
    sortAuthor() {
      return this.myPropCopy.sort((a, b) =>
        a.author.toLowerCase() > b.author.toLowerCase() ? 1 : -1
      );
    },
  },
  mounted() {
    this.sortTitle();
  },
};
</script>

<style>
.mylist {
  cursor: pointer;
}
.mylist:hover {
  padding: 4px;
  background: #e9e524;
  font-weight: bold;
}
div p {
  margin: 8px 0 0;
}
#adding {
  background: #f0f0f0;
  border-radius: 3%;
  border-style: solid;
  border-color: black;
}
</style>

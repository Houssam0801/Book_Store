<template>
  <div>
    <MyHeader :myBooks="myBooks" @handledata="handleInput" />

    <OurButtons :myBooks="myBooks" />

    <div class="container mt-3">
      <div class="row">
        <div class="col-9 mx-auto">
          <div
            id="card"
            class="card text-start mt-2 p-2"
            v-for="(book, index) in filterBooks"
            :key="book.id"
          >
            <div v-if="!book.editing">
              <div class="d-flex justify-content-between">
                <h2>{{ book.title }}</h2>
                <p id="genre" class="fw-bold px-1">{{ book.genre }}</p>
              </div>
              <p class="card-text">
                {{ book.content }}
              </p>
              <div class="d-flex justify-content-between">
                <p class="fw-lighter fst-italic m-0">{{ book.author }}</p>
                <div>
                  <button
                    @click="editBook(index)"
                    type="button"
                    class="btn btn-light py-0 px-2 me-1"
                  >
                    Edit
                  </button>
                  <button
                    @click="deleteEvent(index)"
                    type="button"
                    class="btn btn-outline-danger py-0 px-2"
                  >
                    <i class="bi bi-trash-fill"></i>
                  </button>
                </div>
              </div>
            </div>
            <form v-else @submit.prevent="saveBook(index)">
              <div>
                <p><label for="title">Title:</label></p>
                <input
                  type="text"
                  class="d-inline-flex focus-ring focus-ring-primary py-1 px-2 text-decoration-none border rounded-2 w-50"
                  v-model="myBooks[index].title"
                />
              </div>

              <div>
                <p><label for="content">Content:</label></p>
                <textarea
                  type="text"
                  rows="3"
                  class="d-inline-flex focus-ring focus-ring-primary py-1 px-2 text-decoration-none border rounded-2 w-50"
                  v-model="myBooks[index].content"
                ></textarea>
              </div>

              <div>
                <p><label for="genre">Genre:</label></p>
                <input
                  type="text"
                  class="d-inline-flex focus-ring focus-ring-primary py-1 px-2 text-decoration-none border rounded-2"
                  v-model="myBooks[index].genre"
                />
              </div>

              <div>
                <p><label for="author">Author:</label></p>
                <input
                  type="text"
                  class="d-inline-flex focus-ring focus-ring-primary py-1 px-2 text-decoration-none border rounded-2"
                  v-model="myBooks[index].author"
                />
              </div>
              <div v-if="false">
                <input
                  type="text"
                  class="d-inline-flex focus-ring focus-ring-primary py-1 px-2 text-decoration-none border rounded-2"
                  v-model="myBooks[index].editing"
                  value="false"
                />
              </div>

              <div class="text-center">
                <button class="btn btn-success" type="submit">Save</button>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import MyHeader from "./MyHeader.vue";
import OurButtons from "./OurButtons.vue";

export default {
  data() {
    return {
      myBooks: [
        {
          id: 1,
          title: "The Laws Of Human Nature",
          genre: "General",
          content:
            "If you come across any special trait of meanness or stupidity . . . you must be careful not to let it annoy or distress you.",
          author: "Junkybooks",
          editing: false,
        },
        {
          id: 2,
          title: "The After House",
          genre: "Thriller",
          content:
            "An astonishing story of love and mystery, which equals if not surpasses in interest those other lively stories of Mrs. Rinehart's.",
          author: "Mary Roberts Rinehart",
          editing: false,
        },
        {
          id: 3,
          title: "Becoming",
          genre: "General",
          content:
            "March 2017 hen I was a kid, my aspirations were simple. I wanted a dog. I wanted a house that had stairs in it—two floors for one family.",
          author: "Michelle Obama",
          editing: false,
        },
        {
          id: 4,
          title: "Fire & Water",
          genre: "Adventure",
          content:
            "Mixing magic and inexperience may result in dragons! Khaly accidentally brought her school project to life. And now she has a dragon.",
          author: "Bobbi Schemerhorn",
          editing: false,
        },
      ],
      newFilter: "",
    };
  },
  methods: {
    handleInput(data) {
      this.newFilter = data;
    },

    deleteEvent: function (index) {
      this.myBooks.splice(index, 1);
    },
    editBook(index) {
      this.myBooks[index].editing = true;
    },
    saveBook(index) {
      // Save the book data to the server or local storage
      this.myBooks[index].editing = false;
    },
  },
  computed: {
    filterBooks() {
      let filter = new RegExp(this.newFilter, "i");
      return this.myBooks.filter((el) => el.title.match(filter));
    },
  },

  components: {
    OurButtons,
    MyHeader,
  },
  name: "PageContent",
};
</script>

<style scoped lang="scss">
#genre {
  background: #e9e524;
}
#card {
  background: #f0f0f0;
}
</style>

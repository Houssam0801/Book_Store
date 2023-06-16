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
            v-for="(Book, index) in filterBooks"
            :key="Book.title"
          >
            <div class="d-flex justify-content-between">
              <h2>{{ Book.title }}</h2>
              <p id="genre" class="fw-bold px-1">{{ Book.genre }}</p>
            </div>
            <p class="card-text">
              {{ Book.content }}
            </p>
            <div class="d-flex justify-content-between">
              <p class="fw-lighter fst-italic m-0">{{ Book.author }}</p>
              <div>
                <button type="button" class="btn btn-light py-0 px-2 me-1">
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
          title: "The Laws Of Human Nature",
          genre: "General",
          content:
            "If you come across any special trait of meanness or stupidity . . . you must be careful not to let it annoy or distress you.",
          author: "Junkybooks",
        },
        {
          title: "The After House",
          genre: "Thriller",
          content:
            "An astonishing story of love and mystery, which equals if not surpasses in interest those other lively stories of Mrs. Rinehart's.",
          author: "Mary Roberts Rinehart",
        },
        {
          title: "Becoming",
          genre: "General",
          content:
            "March 2017 hen I was a kid, my aspirations were simple. I wanted a dog. I wanted a house that had stairs in it—two floors for one family.",
          author: "Michelle Obama",
        },
        {
          title: "Fire & Water",
          genre: "Adventure",
          content:
            "Mixing magic and inexperience may result in dragons! Khaly accidentally brought her school project to life. And now she has a dragon.",
          author: "Bobbi Schemerhorn",
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

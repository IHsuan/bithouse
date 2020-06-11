<template>
  <div id="app">
    <div class="container">
      <!-- 搜尋 -->
      <form @submit.prevent class="sticky-top py-3">
        <div class="input-group">
          <div class="input-group-prepend">
            <button type="submit" class="btn btn-outline-secondary">
              <i class="fa fa-search" aria-hidden="true"></i>
            </button>
          </div>
          <input
            type="text"
            v-model="form.keyword"
            class="form-control"
            placeholder="Search"
          />
        </div>
      </form>

      <!-- 分類＆專輯 -->
      <div v-for="category in $list" :key="category.id" class="mb-5">
        <h3>
          {{ category.title }}
        </h3>

        <div class="row">
          <div
            v-for="album in category.albums"
            :key="album.id"
            class="col-4 col-md-3 col-lg-2"
          >
            <figure class="position-relative">
              <img
                :src="album.picture"
                class="img-fluid rounded"
                :alt="album.name"
              />

              <figcaption class="position-absolute text-center">
                {{ album.name }}
              </figcaption>
            </figure>
          </div>

          <!-- 查無結果 -->
          <div class="col-12" v-if="!category.albums.length">
            <p class="text-center text-secondary">
              no result...
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        keyword: "",
      },

      fakeList: [],
    };
  },
  computed: {
    $list() {
      const list = JSON.parse(JSON.stringify(this.fakeList));

      list.forEach((category) => {
        category.albums = category.albums.filter((album) => {
          return album.name.indexOf(this.form.keyword) !== -1;
        });
      });

      return list;
    },
  },

  mounted() {
    const fakeList = [];

    // 三個分類
    for (let i = 1; i <= 3; i++) {
      const category = new Category();

      category.id += i;
      category.title += i;

      // 每個分類十張專輯
      for (let j = 1; j <= 10; j++) {
        const album = new Album();

        const randomNumber = Math.floor(Math.random() * 15) + 1;

        album.id += j;
        album.name += randomNumber;
        album.picture += randomNumber;

        category.albums.push(album);
      }

      fakeList.push(category);
    }

    this.fakeList = fakeList;
  },
};

class Category {
  id = 0;
  title = "title";
  albums = [];
}

class Album {
  id = 0;
  name = "name";
  picture = "https://fakeimg.pl/1000x1000/aaa/?text=picture";
}
</script>

<style lang="scss">
body {
  font-family: "Oswald";
  font-size: 18px;

  @media (max-width: 767px) {
    font-size: 12px;
  }
}

.container {
  padding: 0 1em;
}

.row {
  margin: 0 -0.5em;
}

[class*="col"] {
  padding: 0 0.5em;
}

form {
  background-color: #fff;
}

h3 {
  font-size: 2em;
}

figure {
  margin-bottom: 1em;
}

figcaption {
  left: 0;
  top: 50%;
  transform: translateY(-50%);
  width: 100%;
  font-size: 1.5em;
  text-shadow: 2px 2px #000;
  color: #fff;
}
</style>

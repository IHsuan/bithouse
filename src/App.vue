<template>
  <div id="app">
    <div class="container">
      <form @submit.prevent class="sticky-top py-3">
        <div class="input-group">
          <div class="input-group-prepend">
            <button type="submit" class="btn btn-outline-secondary">
              <i class="fa fa-search" aria-hidden="true"></i>
            </button>
          </div>
          <input type="text" class="form-control" placeholder="Search" />
        </div>
      </form>

      <div v-for="i in 3" :key="i" class="mb-5">
        <h3>
          title {{ i }}
        </h3>

        <div class="row">
          <div v-for="j in 10" :key="j" class="col-4 col-md-3 col-lg-2">
            <figure class="position-relative">
              <img
                src="https://fakeimg.pl/1000x1000/aaa/?text=picture"
                class="img-fluid rounded"
                alt=""
              />

              <figcaption class="position-absolute text-center">
                picture {{ i }} - {{ j }}
              </figcaption>
            </figure>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
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

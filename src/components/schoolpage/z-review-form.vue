<template>
  <div class="flex flex-col text-center">
    <h1>Podelte sa o svoj nazor</h1>
    <form @submit.prevent="onCreateReview">
      <div class="flex flex-col items-center">
        <input
          class="w-1/3 border-2 border-purple-primary focus:outline-none text-purple-primary focus:border-purple-500 focus:ring-border-pink-500 focus:ring-1 rounded-lg p-2"
          placeholder="Ja si o tejto skole myslím..."
          type="text"
          v-model="review"
        />
        <star-rating @update:rating="setRating" :star-size="40"></star-rating>
        <button class="border p-2 my-6" type="submit">Odoslať</button>
        {{ rating }}
      </div>
    </form>
  </div>
</template>

<script>
import axios from "axios";
import StarRating from 'vue-star-rating';

export default {
  data() {
    return {
      review: "",
      rating: 0,
    };
  },
  props: {
    id: String,
  },
  components: {
    StarRating,
  },
   computed: {
    user() {
      return this.$store.getters["user"];
    },
  },
  methods: {
    setRating(rating) {
      this.rating = rating;
    },
    onCreateReview() {
      axios
        .post(`/api/rating`, {
          collage_id: Number(this.id),
          user_id: user.id,
          rating: this.rating,
          body: this.review,
        })
        .then((response) => {
          this.$emit("createReview", response.data.rating);

          this.review = "";
          this.setRating(0);
        });
    },
  },
};
</script>

<style></style>

<template>
  <div>

    <b-modal id="deleteMovieModal" title="Movie Entry" ok-title="Delete Movie" @ok="onDelete" ok-variant="danger">
      Are you sure about deleting this movie? <br><br>
      <h5>{{ movie.title }}</h5>
      <p><i>{{movie.description}}</i></p>
    </b-modal>
  </div>
</template>

<script>
export default {
  props: {
    movie: {}
  },
  methods: {
    async onDelete() {
      this.$axios.delete('/api/movies/' + this.movie.id)
      .then((res)=>{
        if(res.status==202) {
          alert('Movie is deleted successfully!')
          this.$emit('onDeleted')
        }
      })
    }
  }
}
</script>

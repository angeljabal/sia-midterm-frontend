<template>
    <div>
        <b-button v-b-modal.movieEntryModal variant="success">Add Movie</b-button>
        <b-modal id="movieEntryModal" title="Movie Entry" ok-title="Save" @ok="onSubmit">
        <form action="#">
            <b-form-group label="Title" label-for="title">
            <b-form-input id="title" v-model="movie.title" trim></b-form-input>
            </b-form-group>

            <b-form-group label="Description" label-for="description">
            <b-form-input id="description" v-model="movie.description" trim></b-form-input>
            </b-form-group>

            <b-form-group label="Genre" label-for="genre">
            <b-form-input id="genre" v-model="movie.genre" trim></b-form-input>
            </b-form-group>

            <b-form-group label="Year" label-for="year">
            <b-form-input id="year" v-model="movie.year" trim></b-form-input>
            </b-form-group>

            <b-form-group label="Status" label-for="status">
            <b-form-select v-model="movie.status" :options="statuses"></b-form-select>
            </b-form-group>

        </form>
        </b-modal>
    </div>
</template>

<script>
export default {
    data(){
        return{
            movie: {},
            statuses: [
                {value: 'unwatched', text: 'Unwatched'},
                {value: 'unfinished', text: 'Unfinished'},
                {value: 'Completed', text: 'Completed'},
            ]
        }
    },
    methods: {
    async onSubmit() {
      this.$axios.post('/api/movies', this.movie)
      .then((res)=>{
        if(res.status==202) {
          alert('Successfully added the movie')
          this.$emit('onAdd')
        }
      })
    }
  }
}
</script>
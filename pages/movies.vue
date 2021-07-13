<template>
    <div>
        <Navbar />
        <EditMovieModal :movie="selectedMovie" />
        <DeleteMovieModal :movie="selectedMovie" @onDeleted="getAll" />
        <div class="container">
            <h1>
                Watch List
                <movieEntryModal class="float-right" @onAdd="getAll" />
            </h1>
            <table class="table table-bordered tabled-striped">
                <thead>
                <tr class="bg-info text-white">
                    <th>Title</th>
                    <th>Description</th>
                    <th>Genre</th>
                    <th>Year</th>
                    <th>Status</th>
                    <th>&nbsp;</th>
                </tr>
                </thead>
                <tbody>
                    <tr v-for="movie in movies" :key="movie.id">
                        <td>{{movie.title}}</td>
                        <td>{{movie.description}}</td>
                        <td>{{movie.genre}}</td>
                        <td>{{movie.year}}</td>
                        <td>{{movie.status}}</td>
                         <td>
                            <b-button @click="onEdit(movie)" variant="info" size="sm" style="margin: 2px">
                            Edit
                            </b-button>
                            <b-button @click="onDelete(movie)" variant="danger" size="sm" style="margin: 2px">
                            Delete
                            </b-button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return{
            movies: [],
            selectedMovie: {}
        }
    },
    methods: {
        async getAll(){
            await this.$axios.get('/api/movies')
            .then((res)=>{
                if(res.status==200){
                    this.movies = res.data
                }
            })
        },
        onEdit(selectedMovie) {
            this.selectedMovie = selectedMovie
            this.$bvModal.show('editMovieModal')
        },
        onDelete(selectedMovie) {
            this.selectedMovie = selectedMovie
            this.$bvModal.show('deleteMovieModal')
        }
    },
    created() {
        this.getAll()
    },
    
    
}
</script>
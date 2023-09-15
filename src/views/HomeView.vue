<template>
  <div class="home">
    <div class="feature-card">
      <RouterLink to="/movie/tt0268093">
        <img src="../assets/ramayan1.jpg" alt="Ramayan" class="featured-img" />
        <div class="detail">
          <h3>Ramayan</h3>
        </div>
      </RouterLink>
    </div>
    <form @submit.prevent="SearchMovies()" class="search-box">
      <input
        type="text"
        placeholder="What are you looking for?"
        v-model="search"
      />
      <input type="submit" value="Search" />
    </form>

    <div class="Movie-category">
      <input
        type="button"
        value="Marathi movies"
        class="category-button"
        @click="
          selectedCategory = 'Marathi movies';
          initializeMovies(selectedCategory);
        "
      />
      <input
        type="button"
        value="Hindi movies"
        class="category-button"
        @click="
          selectedCategory = 'Hindi movies';
          initializeMovies(selectedCategory);
        "
      />
      <input
        type="button"
        value="South movies"
        class="category-button"
        @click="
          selectedCategory = 'South movies';
          initializeMovies(selectedCategory);
        "
      />
      <input
        type="button"
        value="English movies"
        class="category-button"
        @click="
          selectedCategory = 'English movies';
          initializeMovies(selectedCategory);
        "
      />
    </div>

    <div class="movie-hindi"> Movies</div>
    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-image">
            <img class="movie-image2" :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  data() {
    return {
      movieList: [],
    };
  },
  setup() {
    const search = ref("");
    const movies = ref([]);
    const selectedCategory = ref(""); // Add a property to track the selected category

    const marathiMovies = [
      // Marathi movie objects here
      {
        Title: "Sairat",
        Year: "2016",
        imdbID: "tt5312232",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMjBjNWYyY2UtOGNjZC00MTg4LWIwYWItYmZiNDI5MGUwNWRkXkEyXkFqcGdeQXVyNjI1NjA5NjE@._V1_SX300.jpg",
      },
      {
        Title: "Duniyadari",
        Year: "2013",
        imdbID: "tt3121604",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BZmE2NjM0MzEtYzUxOC00MzlhLTllMTMtZGQ5YzA1MjJkN2U5XkEyXkFqcGdeQXVyODE5NzE3OTE@._V1_SX300.jpg",
      },
      {
        Title: "Ved",
        Year: "2022",
        imdbID: "tt20854842",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BZWJmY2EyODAtMjUwMi00MzdkLTgyNGItZmQ0YzEwOTNiMjk4XkEyXkFqcGdeQXVyODE5NzE3OTE@._V1_SX300.jpg",
      },
      {
        Title: "Mulshi Pattern",
        Year: "2018",
        imdbID: "tt9310280",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BZTY0ZTI0Y2EtMjhmNy00ODQ0LThkN2YtMWU4OTQwNTFiYjUzXkEyXkFqcGdeQXVyNjE1OTQ0NjA@._V1_SX300.jpg",
      },
      {
        Title: "Zapatlela",
        Year: "1993",
        imdbID: "tt0233979",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMzNiNjgzMjMtY2Q1MS00OTI5LWI2MzItNzZjNzU0MDhiNmE4XkEyXkFqcGdeQXVyMzU0NzkwMDg@._V1_SX300.jpg",
      },
      {
        Title: "Chandramukhi",
        Year: "2022",
        imdbID: "tt13206784",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BYzFjYzI4ZDItZDU5OC00YmI4LThiZWMtYTFkMDM3M2VlN2FkXkEyXkFqcGdeQXVyNjkwOTg4MTA@._V1_SX300.jpg",
      },
      {
        Title: "Ashi Hi Banwa Banwi",
        Year: "1988",
        imdbID: "tt0267277",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BZWFjZjFiYTctZTBmZC00MWVmLThkM2UtMGRiNjkxMzZlY2QwXkEyXkFqcGdeQXVyMzU0NzkwMDg@._V1_SX300.jpg",
      },
      {
        Title: "Zapatlela 2",
        Year: "2013",
        imdbID: "tt3319518",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BN2FmZWQ5OGItZDk5Zi00NTUzLWE0YWItYjBlNzFiMzlmYWIzXkEyXkFqcGdeQXVyNjk0NTE3NDM@._V1_SX300.jpg",
      },
      {
        Title: "Patil",
        Year: "2018",
        imdbID: "tt9176214",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BNjgxOGQ1NjktZjk1OS00Y2Q0LTg4NzQtNDAxN2RlOWU0YjhhXkEyXkFqcGdeQXVyOTQ0MjEzMTA@._V1_SX300.jpg",
      },
      {
        Title: "Dombivli Fast",
        Year: "2005",
        imdbID: "tt0833444",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BOWEzZjVjYzQtYzA4Mi00ZmIzLWFmYTMtNDU1N2U5ODM1MTUyXkEyXkFqcGdeQXVyMzA5NzAyMDU@._V1_SX300.jpg",
      },
      {
        Title: "Boyz 3",
        Year: "2022",
        imdbID: "tt21446256",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMTFmYjcxOTgtN2U0Zi00NDZkLTg3NjQtMzViYmQ2NTlhMTYzXkEyXkFqcGdeQXVyMTA2MDAyMDAz._V1_SX300.jpg",
      },
      {
        Title: "Timepass 3",
        Year: "2022",
        imdbID: "tt21345566",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BOWIxMWVlNTEtMjg3YS00NDI0LTlmNTYtYTk2MGJhMzBkYTVhXkEyXkFqcGdeQXVyMTIyNzY0NTMx._V1_SX300.jpg",
      },
      {
        Title: "Ye Re Ye Re Paisa 2",
        Year: "2019",
        imdbID: "tt8983182",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BNzUwOTBjYzMtMDBlYi00YjQ4LTkwN2UtN2JmYTE4NzIzZjZjXkEyXkFqcGdeQXVyODE5NzE3OTE@._V1_SX300.jpg",
      },
      {
        Title: "Morcha marathi movie",
        Year: "2017",
        imdbID: "tt7550794",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMTI4ZTUyZDItOWI4OC00MzQyLTkzMDItZjA5NTg0NTJmYzczXkEyXkFqcGdeQXVyNDY5MTIxNDk@._V1_SX300.jpg",
      },

      {
        Title: "Faktt Marathi",
        Year: "2016",
        imdbID: "tt6059324",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BYmRiNTY1YzUtNmYwYy00ZDBiLTg3MmUtZWY2YjBhYmMwZjY4XkEyXkFqcGdeQXVyNTM4OTA1MTA@._V1_SX300.jpg",
      },

      {
        Title: "Aamhi Bolato Marathi Movie",
        Year: "2014",
        imdbID: "tt10477926",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BOWQwY2VmZGEtNzcxMi00NzIwLWFkNDctMTJjMmE4NWZhNGI2XkEyXkFqcGdeQXVyMTA0MTMyOTIy._V1_SX300.jpg",
      },
      {
        Title: "Mulga (Marathi Movie)2010",
        Year: "2010",
        imdbID: "tt10530804",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BZTFjNzJkZTYtZWY0YS00MjQ0LWExNmUtODJmM2RlMzg0M2U2XkEyXkFqcGdeQXVyMjgxMjcyODk@._V1_SX300.jpg",
      },
      {
        Title: "Kanha",
        Year: "2016",
        imdbID: "tt5985026",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMjkzZjUxMDItM2ZiZi00MjNhLTg4NTktMWNhYTUxZDgzZWRmXkEyXkFqcGdeQXVyNjg0MTc3MTQ@._V1_SX300.jpg",
      },
    ];

    const hindiMovies = [
      // Hindi movie objects here
      {
        Title: "Hindi Medium",
        Year: "2017",
        imdbID: "tt5764096",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BY2E4NWQ4ZjEtNThlOC00NThjLThmZjgtMWU0MDgzMmYwOGU3XkEyXkFqcGdeQXVyODE5NzE3OTE@._V1_SX300.jpg",
      },
      {
        Title: "Film Hindi",
        Year: "2004",
        imdbID: "tt0406774",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BZWZjMmU2NTQtMWYxZi00YThkLTkwN2YtMmYwNTQ1MWFiMzQ3XkEyXkFqcGdeQXVyMjQ0ODM4MDU@._V1_SX300.jpg",
      },
      {
        Title: "Wedding tayo, wedding hindi!",
        Year: "2011",
        imdbID: "tt2027274",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BZWQwOTAyN2EtNmJhOS00Yjg4LTg3YWEtMmU5NmI2MTBhMGZkXkEyXkFqcGdeQXVyNTI5NjIyMw@@._V1_SX300.jpg",
      },
      {
        Title: "'Di puwedeng hindi puwede!",
        Year: "1999",
        imdbID: "tt0336281",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMGUyN2RhZGQtYzA1ZS00NGJhLThkMTctN2E5ZmQ1MGYwNmZhXkEyXkFqcGdeQXVyNDkwMzY5NjQ@._V1_SX300.jpg",
      },
      {
        Title: "Hindi pa tapos ang laban",
        Year: "1994",
        imdbID: "tt0444170",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMGNjMmNmN2QtNzNkOS00MjAxLThiN2QtNzJmZjE1YjUwY2IyXkEyXkFqcGdeQXVyNjgyMzUzMDg@._V1_SX300.jpg",
      },
      {
        Title: "Sakaling hindi makarating",
        Year: "2016",
        imdbID: "tt5586322",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BZmEyYzhjMDgtNGI0YS00MmMwLWJlMzYtZDA0Y2Q3MzFiMzNlXkEyXkFqcGdeQXVyNTI5NjIyMw@@._V1_SX300.jpg",
      },
      {
        Title: "Ang pamilyang hindi lumuluha",
        Year: "2017",
        imdbID: "tt7147654",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMDE0YWUwZjItNWE0MC00YjRlLWE2N2UtZWVjY2UyMDMzZTZhXkEyXkFqcGdeQXVyNTI5NjIyMw@@._V1_SX300.jpg",
      },
      {
        Title: "Hindi magbabago",
        Year: "1994",
        imdbID: "tt0466019",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BNTRiNDcxYzUtZDI4YS00YTA3LTk0NzYtN2U2M2QwYTc1MmEyXkEyXkFqcGdeQXVyNDkwMzY5NjQ@._V1_SX300.jpg",
      },
      {
        Title: "Hindi pa tapos ang labada, darling",
        Year: "1994",
        imdbID: "tt0411487",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BNGY4ODA3NjEtODlhOS00MzIzLTliYWMtNjljY2NhOTY3MzA4XkEyXkFqcGdeQXVyNDkwMzY5NjQ@._V1_SX300.jpg",
      },
      {
        Title: "Parang kayo pero hindi",
        Year: "2021",
        imdbID: "tt14064076",
        Type: "series",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMWJlZTJjZjAtYTQyNS00MDU1LTg0MDgtZjgyMzllMWRiMjFiXkEyXkFqcGdeQXVyNTI5NjIyMw@@._V1_SX300.jpg",
      },
    ];

    const southMovies = [
      {
        Title: "Baahubali: The Beginning",
        Year: "2015",
        imdbID: "tt2631186",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BYWVlMjVhZWYtNWViNC00ODFkLTk1MmItYjU1MDY5ZDdhMTU3XkEyXkFqcGdeQXVyODIwMDI1NjM@._V1_SX300.jpg",
      },
      {
        Title: "Dear Comrade",
        Year: "2019",
        imdbID: "tt8388508",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMTdiNmVmOTAtMDNhZi00OTA1LWJhODEtNGE0ZmE2YjgxN2Y2XkEyXkFqcGdeQXVyODIwMDI1NjM@._V1_SX300.jpg",
      },
      {
        Title: "RRR",
        Year: "2022",
        imdbID: "tt8178634",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BODUwNDNjYzctODUxNy00ZTA2LWIyYTEtMDc5Y2E5ZjBmNTMzXkEyXkFqcGdeQXVyODE5NzE3OTE@._V1_SX300.jpg",
      },
      {
        Title: "Valimai",
        Year: "2022",
        imdbID: "tt10806040",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BOTFjYzEzMzUtNzk2My00ODcwLWIwZTMtZDZkZDkxYWI5NjRkXkEyXkFqcGdeQXVyMTY0MDk0NjE3._V1_SX300.jpg",
      },
      {
        Title: "U Turn",
        Year: "2018",
        imdbID: "tt8733898",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMmIxZjU2NDktNzQzNC00ZjM1LWE5YmYtNTUyNmVkZGU3MzFjXkEyXkFqcGdeQXVyMTEzNzg0Mjkx._V1_SX300.jpg",
      },
      {
        Title: "Major",
        Year: "2022",
        imdbID: "tt9851854",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BYWI2ODNjMDktZjcxNS00YThkLTljMDUtMGIyOTg3ZjY2MjlhXkEyXkFqcGdeQXVyODE5NzE3OTE@._V1_SX300.jpg",
      },
      {
        Title: "Varisu",
        Year: "2023",
        imdbID: "tt11998558",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BYzQ1NmM3NTktY2RmMS00NzgxLWFiZjktM2JjYzY5N2IxNmIzXkEyXkFqcGdeQXVyMTMzNzIyNDc1._V1_SX300.jpg",
      },
      {
        Title: "Yashoda",
        Year: "2022",
        imdbID: "tt15710136",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BZWIwOTdiYjQtOTcwZS00OWE3LWI4ZGYtMDcwMTgxMWIzOTI1XkEyXkFqcGdeQXVyMTEzNzg0Mjkx._V1_SX300.jpg",
      },
      {
        Title: "Virupaksha",
        Year: "2023",
        imdbID: "tt24059780",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BZWExYjRmZjQtZTk5MS00YjM2LTgwOTEtODFmMmQ3ZjlhYzRiXkEyXkFqcGdeQXVyMTYyNjAzOTUx._V1_SX300.jpg",
      },
      {
        Title: "Veeran",
        Year: "2023",
        imdbID: "tt15163636",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BNjQ3MDcxMzAtNjZhYy00ZTQ4LTgzNDEtNDE0YmY4ZDFhODU3XkEyXkFqcGdeQXVyMTQ3Mzk2MDg4._V1_SX300.jpg",
      },
      {
        Title: "North & South: Book 1, North & South",
        Year: "1985",
        imdbID: "tt0088583",
        Type: "series",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BZjdlZTExMTgtY2Q3Ny00NmU4LTgxOTUtZWIyMjBjOTZjMGU3XkEyXkFqcGdeQXVyNTE1NjY5Mg@@._V1_SX300.jpg",
      },
      {
        Title: "Vikram Vedha",
        Year: "2017",
        imdbID: "tt6148156",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BY2FiMTFmMzMtZDI2ZC00NDQyLWExYTUtOWNmZWM1ZDg5YjVjXkEyXkFqcGdeQXVyODIwMDI1NjM@._V1_SX300.jpg",
      },
    ];

    const englishMovie = [
     {
            "Title": "American Beauty",
            "Year": "1999",
            "imdbID": "tt0169547",
            "Type": "movie",
            "Poster": "https://m.media-amazon.com/images/M/MV5BNTBmZWJkNjctNDhiNC00MGE2LWEwOTctZTk5OGVhMWMyNmVhXkEyXkFqcGdeQXVyMTMxODk2OTU@._V1_SX300.jpg"
        },
      {
        Title: "Johnny English",
        Year: "2003",
        imdbID: "tt0274166",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BNDkxODhlNmItYjhiMC00ZjNmLWE2YmMtOTQ3NmQxM2YzOGFiXkEyXkFqcGdeQXVyNTIzOTk5ODM@._V1_SX300.jpg",
      },
      {
        Title: "Johnny English Reborn",
        Year: "2011",
        imdbID: "tt1634122",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMTc0MTM3NzEzMl5BMl5BanBnXkFtZTcwNjE5MTU3NQ@@._V1_SX300.jpg",
      },
      {
        Title: "Johnny English Strikes Again",
        Year: "2018",
        imdbID: "tt6921996",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMGY1ZWUzMzktZDIzZS00ZGJkLTg1MGEtNTQyYWY4ODBlNGZhXkEyXkFqcGdeQXVyNDQ0MTYzMDA@._V1_SX300.jpg",
      },
      {
            "Title": "Avengers: Infinity War",
            "Year": "2018",
            "imdbID": "tt4154756",
            "Type": "movie",
            "Poster": "https://m.media-amazon.com/images/M/MV5BMjMxNjY2MDU1OV5BMl5BanBnXkFtZTgwNzY1MTUwNTM@._V1_SX300.jpg"
        },
      {
        Title: "The English",
        Year: "2022",
        imdbID: "tt11771270",
        Type: "series",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BODRlMjI1MWMtNjgxZS00MDgyLWJiMDAtYTJlMDI4NmUwODkxXkEyXkFqcGdeQXVyMTUzMTg2ODkz._V1_SX300.jpg",
      },
      {
        Title: "The English Game",
        Year: "2020",
        imdbID: "tt8403664",
        Type: "series",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BZGQzOGJmNTEtNDA3ZS00Yjk1LWJlMmItYzZhOTY3MWM3MjQ1XkEyXkFqcGdeQXVyODQyNDI4ODg@._V1_SX300.jpg",
      },
      {
        Title: "A Very English Scandal",
        Year: "2018",
        imdbID: "tt6938856",
        Type: "series",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BNTQ5NDI0MTQ0MV5BMl5BanBnXkFtZTgwNDEzNTc1NTM@._V1_SX300.jpg",
      },
      {
        Title: "The English Teacher",
        Year: "2013",
        imdbID: "tt2055765",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMTU2MjIwNDA5MF5BMl5BanBnXkFtZTcwMjU2NzEzOQ@@._V1_SX300.jpg",
      },
      {
        Title: "Broken English",
        Year: "2007",
        imdbID: "tt0772157",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMTA2NzMwNjIwMDJeQTJeQWpwZ15BbWU3MDMyNDgzNTE@._V1_SX300.jpg",
      },
    ];

    // Static movie data
    const staticMovies = [
      {
        Title: "Subhedar",
        Year: "2023",
        imdbID: "tt25396050",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BYTZhNjQwOWMtY2Q1Ni00OTcyLWExMzQtZGI0NjE0OGQ2NDJkXkEyXkFqcGdeQXVyNjkwOTg4MTA@._V1_SX300.jpg",
      },
      {
        Title: "Jawan",
        Year: "2023",
        imdbID: "tt15354916",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BZjM2MjE4NWYtOTc1MC00ZDliLWIzYmYtNzNjMTU2Yzg4ODNlXkEyXkFqcGdeQXVyMTUyNjIwMDEw._V1_SX300.jpg",
      },
      {
        Title: "The Nun II",
        Year: "2023",
        imdbID: "tt10160976",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BNmE5MmM2ZGEtNTVlNC00M2Q3LTliMjMtMzg5YjUyMjliZWIzXkEyXkFqcGdeQXVyMTAxNzQ1NzI@._V1_SX300.jpg",
      },
      {
        Title: "Oppenheimer",
        Year: "2023",
        imdbID: "tt15398776",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMDBmYTZjNjUtN2M1MS00MTQ2LTk2ODgtNzc2M2QyZGE5NTVjXkEyXkFqcGdeQXVyNzAwMjU2MTY@._V1_SX300.jpg",
      },
      {
        Title: "Jailer",
        Year: "2023",
        imdbID: "tt11663228",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BNzFkNmZkMTctYjRhMS00ODZiLWFlNjQtZmZmN2IzMDJlNmVkXkEyXkFqcGdeQXVyMTY1MzAyNjU4._V1_SX300.jpg",
      },
      {
        Title: "Gadar 2",
        Year: "2023",
        imdbID: "tt15441054",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BZGEzMDJjNGUtYTFhZi00MDgyLWIzMzYtMzcwMDQyZjcyNGY1XkEyXkFqcGdeQXVyNTcwNTM5ODI@._V1_SX300.jpg",
      },
      {
        Title: "Kushi",
        Year: "2023",
        imdbID: "tt15380630",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BNmU2Nzc2ZmItMTc5ZS00ZTE5LWEyOTMtMzIwYjBkNTI3Mjg4XkEyXkFqcGdeQXVyMTUyNjIwMDEw._V1_SX300.jpg",
      },
      {
        Title: "Ghoomer",
        Year: "2023",
        imdbID: "tt20913276",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMDcwYzg2ZDctNTFjMi00YjliLWFkNmYtOTBkZjQ1YzQ1MTNhXkEyXkFqcGdeQXVyODE5NzE3OTE@._V1_SX300.jpg",
      },
      {
        Title: "Rocky Aur Rani Kii Prem Kahaani",
        Year: "2023",
        imdbID: "tt14993250",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BM2VmOTU2ZmItMGVmMy00NmZmLTk5Y2QtMmI5ODczNDkyZmNjXkEyXkFqcGdeQXVyMTUzNTgzNzM0._V1_SX300.jpg",
      },

      {
        Title: "OMG 2",
        Year: "2023",
        imdbID: "tt15732324",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BNmQ3MThkOWEtNTA0NC00YzI2LWIxZjEtZjdlZTVmNzQ2ZGViXkEyXkFqcGdeQXVyODE5NzE3OTE@._V1_SX300.jpg",
      },
      {
        Title: "Blue Beetle",
        Year: "2023",
        imdbID: "tt9362930",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BMmY1ODUzZGItNDllOS00MDBhLTg4NmUtYjU4YjUxMGNlYmMwXkEyXkFqcGdeQXVyODE5NzE3OTE@._V1_SX300.jpg",
      },
      {
        Title: "The Black Demon",
        Year: "2023",
        imdbID: "tt10279472",
        Type: "movie",
        Poster:
          "https://m.media-amazon.com/images/M/MV5BODBhZTFiOGItNjk4ZS00Y2VkLWJkNGQtNTk5NzZlNThlM2I4XkEyXkFqcGdeQXVyMzQwMTY2Nzk@._V1_SX300.jpg",
      },
      // Add more static movie objects here
    ];

    // Initialize movies with static data based on the selected category
    const initializeMovies = (category) => {
      switch (category) {
        case "Marathi movies":
          movies.value = marathiMovies;
          break;
        case "Hindi movies":
          movies.value = hindiMovies;
          break;
        case "South movies":
          movies.value = southMovies;
          break;
        case "English movies":
          movies.value = englishMovie;
          break;
        default:
          movies.value = staticMovies;
      }
    };

    // Initialize movies based on the default selected category (e.g., Marathi movies)
    initializeMovies(selectedCategory.value);

    // Initialize movies with static data
    movies.value = staticMovies;

    const SearchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=dd3365fb&s=${search.value}`)
          .then((response) => response.json())
          .then((data) => {
            console.log(data);
            movies.value = data.Search;
            search.value = "";
          });
      }
    };

    return {
      search,
      movies,
      SearchMovies,
      selectedCategory,
      initializeMovies,
    };
  },
};
</script>

<style lang="scss">
.home {
  max-width: 1200px;
  margin: auto;
  .feature-card {
    position: relative;
    overflow-x: hidden;
    white-space: nowrap;
    margin-top: auto;

    .featured-img {
      display: block;
      width: 100%;
      height: 300px;
      object-fit: cover;
      position: relative;
      z-index: 0;
    }

    .detail {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: rgba(0, 0, 0, 0.6);
      padding: 16px;
      z-index: 1;

      h3 {
        color: #fff;
        margin-bottom: 16px;
      }

      p {
        color: #fff;
      }
    }
  }

  .search-box {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 16px;

    input {
      display: block;
      appearance: none;
      border: none;
      outline: none;
      background: none;

      &[type="text"] {
        width: 100%;
        color: #fff;
        background-color: #496583;
        font-size: 20px;
        padding: 10px 16px;
        border-radius: 8px;
        margin-bottom: 15px;
        transition: 0.4s;

        &::placeholder {
          color: #f3f3f3;
        }

        &:focus {
          box-shadow: 0px 3px 6px rgba(0, 0, 0, 0.2);
        }
      }

      &[type="submit"] {
        width: 100%;
        max-width: 300px;
        background-color: #42b883;
        padding: 16px;
        border-radius: 8px;
        color: #fff;
        font-size: 20px;
        text-transform: uppercase;
        transition: 0.4s;

        &:active {
          background-color: #3b8070;
        }
      }
    }
  }

  .Movie-category {
    display: flex;
    flex-wrap: wrap;
    padding: 16px;
    width: 100%;
    border-radius: 8px;
    color: #fff;
    font-size: 20px;
    text-transform: uppercase;
    transition: 0.4s;

    .movie-image2 {
      object-fit: contain;
    }

    /* Style each button individually */
    .category-button {
      width: auto;
      height: auto;
      background-color: gold;
      font-size: larger;
      color: black;
      padding: 10px 20px;
      border: none;
      border-radius: 8px;
      cursor: pointer;
      font-weight: bold;
      transition: background-color 0.3s;

      &:hover {
        background-color: #f53a0c;
      }
    }

    gap: 110px;
    padding: 16px;
    border-radius: 8px;
    color: #fff;
    font-size: 20px;
    text-transform: uppercase;
    transition: 0.4s;
  }

  .movie-hindi {
    display:flex;
    flex-direction: column;
      align-items: center;
    padding: 16px;
    color: #fff;
    border: rgb(234, 229, 229);
    background-color: #110101;
    font-size: 40px;
    margin-bottom: 20px;
    margin-top: 20px;
  }

  .movies-list {
    display: flex;
    flex-wrap: wrap;
    margin: 0px 8px;

    .movie {
      max-width: 50%;
      flex: 1 1 50%;
      padding: 16px 8px;

      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;

        .product-image {
          position: relative;
          display: block;

          img {
            display: block;
            width: 100%;
            height: 275px;
            object-fit: cover;
          }

          .type {
            position: absolute;
            padding: 8px 16px;
            background-color: #42b883;
            color: #fff;
            bottom: 16px;
            left: 0px;
            text-transform: capitalize;
          }
        }

        .detail {
          background-color: #496583;
          padding: 16px 8px;
          flex: 1 1 100%;
          border-radius: 0px 0px 8px 8px;

          .year {
            color: #aaa;
            font-size: 14px;
          }

          h3 {
            color: #fff;
            font-weight: 600;
            font-size: 18px;
          }
        }
      }
    }
  }
}
</style>

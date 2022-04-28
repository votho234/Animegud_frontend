<template>
 <v-container>
  
   <div class="container__item">
		<form class="form">
			<input type="text" id="input" class="form__field" placeholder="" @onkeyup="search" />
			<button @click="search" type="button" class="btn btn--primary btn--inside uppercase">Send</button>
		</form>
	</div>
  
   <v-row >
    <v-col  v-for="post in posts" :key="post.mal_id">
         <v-col class="movie-item">
           <div>
             <v-img :src="`${post.image_url}`"></v-img>
           </div>
           <div class="name">{{post.title}}</div>
        </v-col>
    </v-col>
    </v-row>
 </v-container>
</template>


<script>
import API from "../api";
export default {
    name :"Home",
    data(){
        
    return {

        posts: [],
    };
    },
    
    async created(){
		 this.posts = await API.getAPI("pokemon");
    },
    methods:{
     async search(){
    const input = document.getElementById("input").value;
    console.log("List_of_comprehensive_groups -> "+ input);
     
    this.posts = await API.getAPI(input);

    }
    },
};
</script>
<style lang="scss">

//** variables
$background: #79d6e6;
$text: #9c9c9c;
$input-bg-color: #fff;
$input-text-color: #a3a3a3;
$button-bg-color: #0a7379;
$button-text-color: #fff;

//** root
:root {
	background: $background;
	color: $text;
	font: 1rem "PT Sans", sans-serif;
}

html,
body,
.container {
	height: 100%;
}

a {
	color: inherit;
	
	&:hover {
		color: $button-bg-color;
	}
}

//** helper
.container {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}

.uppercase {
	text-transform: uppercase;
}

//** button
.btn {
	display: inline-block;
	background: transparent;
	color: inherit;
	font: inherit;
	border: 0;
	outline: 0;
	padding: 0;
	transition: all 200ms ease-in;
	cursor: pointer;
	
	&--primary {
		background: $button-bg-color;
		color: $button-text-color;
		box-shadow: 0 0 10px 2px rgba(225, 241, 239, 0.815);
		border-radius: 2px;
		padding: 12px 36px;
		
		&:hover {
			background: darken($button-bg-color, 4%);
		}
		
		&:active {
			background: $button-bg-color;
			box-shadow: inset 0 0 10px 2px rgba(100, 197, 224, 0.2);
		}
	}
	
	&--inside {
		margin-left: -96px;
	}
}

//** form
.form {	
	&__field {
		width: 360px;
		background: #fff;
		color: $input-text-color;
		font: inherit;
		box-shadow: 0 6px 10px 0 rgba(52, 186, 213, 0.1);
		border: 0;
		outline: 0;
		padding: 22px 18px;
	}
}

.movie-item{
  padding: 2px;
  background:rgb(4, 88, 46);
  border: 0px rgb(5, 117, 91);
  border-radius: 5px rgb(37, 223, 192);
}
.movie-item img{
  background: rgb(4, 120, 100);
}
.name{
  text-align: center;
  font-size: medium;
  color:#3348d4;
  background: #f5f6fa;
}
</style>
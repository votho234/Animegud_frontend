<template>
    <v-container>
        <v-row class="mx-auto">
            <v-col sm="30" class="mx-auto">
                <v-card>
                    <v-card-title>Add New Post</v-card-title>
                    <v-divider></v-divider>
                    <v-form ref="form" @submit.prevent="submitForm" class="px-3" enctype="multipart/form-data">
                        <v-text-field label="Title" v-model="post.title" prepend-icon="mdi-note" :rules="rules"></v-text-field>

                        <v-text-field label="Type" v-model="post.type" prepend-icon="mdi-view-list" :rules="rules"></v-text-field>

                        <v-textarea label="Synopsis" v-model="post.synopsis" prepend-icon="mdi-note-plus" :rules="rules"></v-textarea>

                        <v-text-field label="Score" v-model="post.score" prepend-icon="mdi-star" :rules="rules"></v-text-field>

                        <v-file-input @change="selectFile" :rules="rules" show-size counter multiple label="Select Image"></v-file-input>

                        <v-btn type="submit" class="mt-3" color="primary">Add Post</v-btn>
                    </v-form>
                </v-card>
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
import API from "../api";
export default {
    data(){
        
        return{
            rules: [(value) => !!value || "This field is required"],
           
            post:{
                title:"",
                type:"",
                synopsis:"",
                score:"",
                image:"",
            },
            image: "",
        };
    },
    methods: {
        selectFile(file){
            this.image = file[0];
        },
        async submitForm(){
            const formData = new FormData();
            formData.append("image", this.image);
            formData.append("title", this.post.title);
            formData.append("type", this.post.type);
            formData.append("synopsis", this.post.synopsis);
            formData.append("score", this.post.score);
            if(this.$refs.form.validate()){ 
                const response = await API.addPost(formData);
                this.$router.push({ name:"home", params: {message: response.message } });
            }
        },
    },
};
</script>

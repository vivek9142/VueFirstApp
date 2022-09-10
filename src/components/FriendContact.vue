<template>
    <li>
        <h2>{{name}} {{isFavorite ? "(Favourite)" : ""}}</h2>
        <button @click="toggleFav">Toggle Favorite</button>
        <button @click="toggleDetails">{{detailsAreVisible ? "Hide" : "Show"}}</button>
        <ul v-if="detailsAreVisible">
            <li><strong>Phone:</strong> {{phoneNumber}}</li>
            <li><strong>Email:</strong> {{emailAddress}}</li>
          </ul>
    </li>
</template>

<script>
export default {
    props:{
        id:{type:String,required:true},
        name:{ type: String, required: true},
        phoneNumber:{type:String, required:true},
        emailAddress:String,
        isFavourite: {
            type:Boolean,
            required:false,
            default:false,
        }
    },
    data(){
        return {
            detailsAreVisible:false,
        }
    },
    methods:{
        toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    toggleFav(){
        // this.friendIsFavourite = !this.friendIsFavourite;
        /*
        That's a built in method, which you can call from inside a Vue component under this 
        keyword. And this allows you to emit your own custom event to which you then can 
        listen from inside the parent component. Now emit wants at least one argument,
        and that is the name of the custom event.

        Here the convention is to always use kebab case no matter where you use it.
        So that's different to props where in the component that receives it, you use 
        camel case and you only use kebab case for passing in the values.
        For events it's always kebab case.
        */

        this.$emit('toggle-favourite',this.id);
    }
    }
}
</script>

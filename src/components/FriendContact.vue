<template>
    <li>
        <h2>{{name}} {{friendIsFavourite === "1" ? "(Favourite)" : ""}}</h2>
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
    // props:["name","phoneNumber","emailAddress","isFavourite"],
    //instead of just asking props we can validate them
    props:{
        name:{ type: String, required: true},
        phoneNumber:{type:String, required:true},
        emailAddress:String,
        // isFavourite:{
        //     type:String,
        //     required:false,
        //     default:'0',
        //     validator:function(value){
        //         return value === '1' || value==='0'
        //     }
        // }
        isFavourite: {
            type:Boolean,
            required:false,
            default:false,
        }
    },
    data(){
        return {
            detailsAreVisible:false,
            //2 proc - assign new obj to recieved prop and then change it with this new obj
            friendIsFavourite:this.isFavourite
        }
    },
    methods:{
        toggleDetails() {
      this.detailsAreVisible = !this.detailsAreVisible;
    },
    // toggleFav(){
        // this.isFavourite = !this.isFavourite; 
        // 25:9  error  Unexpected mutation of "isFavourite" prop  vue/no-mutating-props
    // }
    toggleFav(){
        this.friendIsFavourite = this.friendIsFavourite === '0' ? '1' : '0';
    }
    }
}
</script>

/*
Well, let's also see we have another button here, which allows us to change the favorite 
status.I'll say Toggle Favorite on the button.And I'll add a new method.
toggleFavorite could be the name to which I wanna point here
with the click listener on that button. And now we add this method here
in the methods, toggleFavorite.

And in here, I'll check if this isFavorite is equal to one. So if we were a favorite,
in which case I'll set it to zero and otherwise, if isFavorite was zero I'll set it to one.
we could do it as to change the favorite status with help of the button.
If we saved it, we get an error here.The error is unexpected mutation of isFavorite prop.
As I mentioned, that's not something you should do.Now, why should you not do that?
Because Vue uses a concept which is called unidirectional data flow.

it means one simple thing.Data passed from app to friend contact should only be changed in 
app, not in friend contact.We just pass data down to friend contact.
And once the data is passed down,friend contact cannot change the data we manage an app view,
at least not by simply changing the received data.So if we change data inside of friend 
contact like here,when I tried to change isFavorite,this is not allowed by Vue,
because we violate this pattern of having a unidirectional data flow.

Now, if we want to change this,there are two ways of doing that.The first way of doing it, 
is that we let the parent know that we'd like to change this.Then the parent can go ahead 
and change the data in itself and pass the updated data back to friend contact.
It's an important pattern

The other approach is that we simply take the received data as the initial data, inside of 
friend contact,and then we changed that data instead of friend contact,but we are aware of 
the fact that we only change it there and that this won't affect the data in App.vue.

*/ 
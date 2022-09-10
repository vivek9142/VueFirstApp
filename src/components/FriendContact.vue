<template>
    <li>
        <h2>{{name}} {{isFavourite ? "(Favourite)" : ""}}</h2>
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
    emits:['toggle-favourite'],
    // emits:{
    //     'toggle-favourite':function(id){
    //         if(id)  return true;
    //         else {
    //             console.warn('Id is missing');
    //             return false;
    //         }
    //     }
    // },
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
        this.$emit('toggle-favourite',this.id);
    }
    }
}
</script>

/*
You can let Vue know about the events your component will emit.
For props, this is actually required. For events, it's recommended.

Now emits, so to say, is the counterpart to props. In props you will define
which props this component receives. In emits, you will define which custom events
your component will eventually at some point emit. And you're doing this to document your 
component, to make it obvious to other developers, how your component works,
and to which events they can listen.

But just as with props, you can also specify an object instead,
and then add your admitted events as keys here like this, and then provide a more detailed 
configuration. The configuration you should then add is a function, a function that receives 
the data, which you eventually will emit as parameters. So in this case,
we will eventually emit an ID. So here we would add ID as a parameter,
and I'm doing that to make it obvious that "toggle-favorite" is an event that should be 
handled by a function that expects an ID. Because I will emit an ID here.
You can then also add validation here to make sure that when the event is emitted,
this data, which should be part of the event is not forgotten.

if not shared id it will pop out warn console msg 
*/


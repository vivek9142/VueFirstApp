/*
Now we got isFavorite managed here, and of course we can pass that down to our component,
but there, again, it just acts as an initial prop value, which means if I click toggle 
favorite here, that changes it inside of the FriendContact component,
but not inside of our core friends data. Here of course, that is just some dummy data,
but if this would be coming from a database, we probably would want to send it back
to that database as well. So just changing it inside of that component is not enough.

We would also want to change it here in app.vue file in our friends data, in our friends 
array. So therefore, we now need communication from the FriendContact component back to 
app.vue. So basically the opposite of props. 

If a component should talk to its parent and let the parent know that something happened,
that component should emit an event to which the parent can listen. And indeed you can emit 
your own custom events inside of your Vue components.
*/

<template>
    <div>
      <header><h1>My Friends</h1></header>
    <ul>
        <friend-contact 
        v-for="friend in friends"
        :key="friend.id"
        :id="friend.id"
        :name= "friend.name"
        :phone-number= "friend.phone"
        :email-address= "friend.email"
        :is-favourite="friend.isFavourite"
        @toggle-favourite="toggleFavouriteStatus"></friend-contact>
    </ul>
    </div>
</template>

<script>
export default {
    data(){
      return {
        friends: [
        {
          id: "manuel",
          name: "Manuel Lorenz",
          phone: "01234 5678 991",
          email: "manuel@localhost.com",
          isFavourite:true
        },
        {
          id: "julie",
          name: "Julie Jones",
          phone: "09876 543 221",
          email: "julie@localhost.com",
          isFavourite:false
        },
      ],
      }
    },
    methods:{
      toggleFavouriteStatus(friendId){
        console.log(friendId);
        const foundFriend = this.friends.find(friend => friend.id === friendId);
        console.log(foundFriend)
        foundFriend.isFavourite = !foundFriend.isFavourite;
        console.log(this.friends,foundFriend)
      }
    }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Jost&display=swap');
    * {
  box-sizing: border-box;
}

html {
  font-family: 'Jost', sans-serif;
}

body {
  margin: 0;
}

header {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 3rem auto;
  border-radius: 10px;
  padding: 1rem;
  background-color: #58004d;
  color: white;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

#app ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

#app li {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 1rem auto;
  border-radius: 10px;
  padding: 1rem;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

#app h2 {
  font-size: 2rem;
  border-bottom: 4px solid #ccc;
  color: #58004d;
  margin: 0 0 1rem 0;
}

#app button {
  font: inherit;
  cursor: pointer;
  border: 1px solid #ff0077;
  background-color: #ff0077;
  color: white;
  padding: 0.05rem 1rem;
  box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.26);
}

#app button:hover,
#app button:active {
  background-color: #ec3169;
  border-color: #ec3169;
  box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
}

</style>
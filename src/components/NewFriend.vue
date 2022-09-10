<template>
    <form @submit.prevent="submitData">
        <div>
            <label for="name">Name</label>
            <input type="text" v-model='enteredName' id='name'/>
        </div>
        <div>
            <label for="phone">Phone</label>
            <input type="tel" v-model='enteredPhone' id='phone'/>
        </div>
        <div>
            <label for="email">E-mail</label>
            <input type="email" v-model='enteredEmail' id='email'/>
        </div>

        <div>
            <button>Add Contact</button>
        </div>
    </form>
</template>

<script>
export default {
    emits:['add-contact'],
    data(){
        return {
            enteredName:'',
            enteredPhone:'',
            enteredEmail:''
        }
    },
    methods:{
        submitData(){
            this.$emit('add-contact',this.enteredName,this.enteredPhone,this.enteredEmail)
        }
    }
}
</script>
<template>
    <div>
        <!-- Event: Traverse the Components all the way up to the App components where the array is -->
        <form @submit="addTodo">
            <input type="text" name="title" v-model="title" placeholder="Add Todo">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<script>
export default {
    name: 'AddTodo',
    data() {
        return {
            title: ''
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault();
            const newTodo = {
                completed: false,
                title: this.title
            }

            // send up to parent
            this.$emit('add-todo', newTodo);

            // clear the form
            this.title = ''
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
    }

    input[type="text"] {
        flex: 10;
        padding: 5px;
    }

    input[type="submit"] {
        flex: 2;
    }
</style>


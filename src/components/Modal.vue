<template>
    <div id="mask" v-show="showModal">
        <div id="modal-content">
            <h2>Add New To-Do</h2>
            <input type="text" placeholder="Enter new To-Do here" v-model="newTodo">
            <div>
                <button @click="cancelAdd()">Cancel</button>
                <button @click="addTodo()">Add</button>
            </div>
         
        </div>
    </div>
</template>

<script>
export default {
    props: ["todos", "showModal"],
    data() {
        return {
            newTodo: '',
        }
    },
    methods: {
        addTodo() {
            this.todos.push({ content: this.newTodo, isDone: false });
            this.$emit("changevalue", this.todos);
            this.showModal = false;
            this.$emit("changeshow", this.showModal);
        },
        cancelAdd() {
            this.showModal = false;
            this.$emit("changeshow", this.showModal);
        }
    }
}
</script>

<style lang="scss">
    #mask {
        position: absolute;
        top: 0px;
        left: 0px;
        width: 100vw;
        height: 100vh;
        background-color: rgba(255, 255, 255, 0.8);
        display: grid;
        place-items: center;
        #modal-content {
            width: 300px;
            height: 140px;
            background-color: #46A1DE;
            display: flex;
            flex-direction: column;
            align-items: center;
            padding: 10px 10px;
            h2 {
                color: #d64a4b;
                margin-bottom: 10px;
            }
            input {
                display: block;
                width: 85%;
                height: 35px;
                overflow: auto;
                margin-bottom: 15px;
                padding: 0px 10px;
                &:focus {
                    outline: none;
                }
            }
            > div {
                width: 80%;
                display: flex;
                justify-content: space-around;
                button {
                    width: 80px;
                    height: 25px;
                }
            }
        }
    }
</style>
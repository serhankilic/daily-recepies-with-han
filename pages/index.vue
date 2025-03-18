<template>
    <div class="container">
        <video src="/bg-video.mp4" autoplay loop muted class="bg-video" ></video>
        <div class="todo-content">
            <p class="app-title">Han Nuxt Todo</p>
            <div class="todo-container">
                <div class="input-area">
                    <input type="text" v-model="todoText" class="todoInput" placeholder="What i will do?" @keyup.enter="addTodo" style="color:white ">
                    <button  @click="addTodo" class="addButton" >+</button>
                </div>
                <ul class="todo-list-container">
                    <li v-for="(todo, index) in todos" :key="index">
                        <input type="checkbox" v-model="todo.completed" class="checkbox">
                        <span v-if="!todo.editing" :class="{ completed: todo.completed }" class="list-text">{{ todo.text }}</span>
                        <input v-else type="text" v-model="todo.text" class="edit-input" @keyup.enter="saveEdit(index)" @blur="saveEdit(index)"
                        >

                        <button @click="editTodo(index)" class="editButton">Edit</button>
                        <button @click="removeTodo(index)" class="deleteButton">Remove</button>
                    </li>
                </ul>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'
const todoText = ref('')
const todos = ref([])
// serhan gotten veriyo
const addTodo = () => {
    if (todoText.value.trim() !== '') {
        todos.value.push({ text: todoText.value, completed: false, editing: false }) // Düzenleme durumu ekledik
        todoText.value = '' // Input'u temizle
    }
}

const removeTodo = (index) => {
    todos.value.splice(index, 1) // Belirtilen index'teki elemanı sil
}

// edit fonksiyonu
const editTodo = (index) => {
    todos.value[index].editing = true
}

// Düzenlemeyi kaydetme
const saveEdit = (index) => {
    todos.value[index].editing = false
}
</script>

<style>
* {
    margin: 0;
    padding: 0;
}
.container {
    width: 100vw;
    height: 100vh;
    background-color: #023364;
    position: relative;
    padding-top: 8rem;
    .bg-video {
        width: 100vw;
        height: 100vh;
        position: absolute;
        top: 0;
        left: 0;
        mix-blend-mode: lighten;
        opacity: 0.3;
    }
    .todo-content {
        width: fit-content;
        height: fit-content;
        display: flex;
        flex-direction: column;
        justify-content: center;
        row-gap: 50px;
        margin: 0 auto;
        padding: 1rem 2rem;
        border-radius: 20px;
        backdrop-filter: blur(2px);
        .app-title {
            width: fit-content;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 4rem;
            font-family: "SF Pro Display", sans-serif;
            color: white;
            margin: 3rem auto 0;

        }
        .todo-container {
            width: 100%;
            height: 100%;
            display: flex;
            flex-direction: column;
            row-gap: 30px;

            .input-area {
                width: 100%;
                display: flex;
                flex-direction: row;
                column-gap: 10px;
                justify-content: center;
                align-items: center;
                .todoInput {
                    width: 700px;
                    height: 50px;
                    padding-left: 10px;
                    border: 1px solid dimgray;
                    border-radius: 12px;
                    font-size: 16px;
                    transition: .3s all ease-in-out;
                    background-color: #0556a9;
                }
                ::placeholder {
                    color: lightgray;
                    opacity: 1; /* Firefox */
                }

                ::-ms-input-placeholder { /* Edge 12 -18 */
                    color: white;
                }
                .todoInput:focus-within {
                    border: 1px solid white;
                    outline: none;
                }
                .addButton {
                    width: 50px;
                    height: 50px;
                    border-radius: 12px;
                    border: 1px solid lightgray;
                    font-size: 32px;
                    font-family: Arial, sans-serif;
                    text-align: center;
                    font-weight: lighter;
                    background-color: greenyellow;
                }
                .addButton:hover {
                    cursor: pointer;
                }
            }
            .todo-list-container {
                display: flex;
                flex-direction: column;
                row-gap: 20px;
                width: 750px;
                margin: 0 auto;
                justify-content: center;
                align-items: center;
                li {
                    list-style: none;
                    width: 100%;
                    display: flex;
                    flex-direction: row;
                    column-gap: 20px;
                    align-items: center;
                    position: relative;
                    z-index: 2;
                    font-family: "SF Pro Display", sans-serif;
                    .checkbox {
                        width: 30px;
                        height: 30px;
                    }
                    .text {
                        text-align: start;
                        font-size: 24px;
                        color: white;
                    }
                    .list-text {
                        text-align: left;
                        font-size: 24px;
                        color: white;
                    }
                    .deleteButton {
                        width: 80px;
                        height: 40px;
                        font-size: 16px;
                        background-color: darkred;
                        border-radius: 12px;
                        border: 1px solid darkred;
                        color: white;
                        transition: .4s all ease-in-out;
                        z-index: 1;
                        position: absolute;
                        right: 20px;
                    }
                    .deleteButton:hover {
                        cursor: pointer;
                        background-color: red;
                    }
                    .completed {
                        text-decoration: line-through;
                        opacity: 0.6;
                    }
                    .edit-input {
                        font-size: 24px;
                        padding: 5px;
                        width: 200px;
                        border: 1px solid lightgray;
                        border-radius: 6px;
                        background-color: #0556a9;
                        color: white;
                    }

                    .editButton {
                        position: absolute;
                        width: 80px;
                        height: 40px;
                        font-size: 16px;
                        right: 120px;
                        background-color: mediumpurple;
                        border-radius: 12px;
                        border: 1px solid purple;
                        padding: 5px 10px;
                        color: white;
                        cursor: pointer;
                        transition: .3s all ease-in-out;
                    }

                    .editButton:hover {
                        background-color: mediumslateblue;
                    }

                }
            }
        }
    }
}
</style>
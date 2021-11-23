<script>
	import TodoItem from "./TodoItem.svelte";

    let value = ''
    let storage = JSON.parse(localStorage.getItem('Todo'))
    let todoList = storage ? storage : []

    function addTodoItem(){
        todoList = [...todoList,{
            id: Date.now().toFixed(0),
            todo: value,
            status: false
        }]
        localStorage.setItem('Todo', JSON.stringify(todoList))
        value = ''
    }
    function removeTodo(){
       if(todoList.length != 0){
           if(window.confirm('Ви дійсно хочете видалити всі завдання?')){
               todoList = []
               localStorage.clear()
               alert("Усі завдання були видалені)")
           }
       } else {
            alert("На даний момент у вас немає ніяких задач !!!")
        }
    }
    function removeTodoItem(id){
        todoList = todoList.filter(item=> item.id !== id)
        localStorage.setItem('Todo', JSON.stringify(todoList))
    }
    function statusDone(index){
        todoList[index].status = !todoList[index].status
        localStorage.setItem('Todo', JSON.stringify(todoList))
        console.log(todoList)
    }

</script>

<main>
    <h2>TodoList</h2>
    <div class="containerButton">
        <input type="text" bind:value={value}>
        <button on:click={value != '' && addTodoItem} class="add">🟢</button>
        <button on:click={removeTodo}>🔴</button>
    </div>

    {#each todoList as todo, index (todo.id)}
        <TodoItem {...todo} index = {index+1} removeTodoItem = {removeTodoItem} statusDone = {statusDone}/>
        {:else }
        <h1>TodoList Empty !!!</h1>
    {/each}
</main>

<style>
    .containerButton{
        width: 100%;
        display: flex;
        justify-content: center;
    }
   main{
       width: 450px;
       background: #ffff;
       margin:auto;
       padding: 10px;
       display: flex;
       justify-content: center;
       align-items: center;
       flex-direction: column;
       border-radius: 10px;
   }
   input{
       outline: none;
       border-radius: 10px;
       width: 70%;
       cursor: pointer;
       background: #F2F2F2;
   }
   :global(button){
       cursor: pointer;
       background: none;
       border: none;
   }
   .add{
       color: #3af13a;
   }

</style>
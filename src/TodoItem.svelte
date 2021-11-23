<script>
    export let todo = "undefined"
    export let status = "undefined"
    export let index = 0
    export let removeTodoItem
    export let id
    export let statusDone
</script>

<div class="container" on:click={statusDone(index-1)}>
    <div class={status&&"done"}>{index}: {todo}</div>
    <button on:click={()=>{removeTodoItem(id)}}>❌</button>
</div>

<style>
    div.container{
        display: flex;
        justify-content: center;
        align-items: center;
        background: #F2F2F2;
        border-radius: 10px;
        width: 90%;
    }
    div{
        margin: 10px;
        padding: 5px;
        width: 350px;
        cursor: pointer;
    }

    .done{
        text-decoration:line-through;
    }

    button{
        margin: 5px;

    }


</style>
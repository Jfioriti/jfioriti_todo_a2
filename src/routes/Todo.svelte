<script>
  import { text } from "@sveltejs/kit";

let todoItem = $state('');
let todoList = $state([]);

function addItem(event){
     event.preventDefault();
     if (todoItem == '') {
          return;
     }
     todoList = [...todoList,{
          text: todoItem,
          done: false
     }];
     todoItem = '';
}
function removeItem(index) {
     todoList = todoList.toSpliced(index, 1);
}

$inspect(todoList);

</script>
<div class="main">
     <form onsubmit={addItem}>
     <input type="text" bind:value={todoItem}>
     <button type="submit">Add</button>
     </form>


     <ul>
          {#each todoList as item, index}
               <li>
                    <input type="checkbox" bind:checked={item.done}>
                    <span class:done={item.done}>{item.text}</span>
                    <button type="button" onclick={() => removeItem(index)}>x</button>
               </li>
          {/each}
     </ul>
</div>
<style>
     ul{
          list-style: none;
     }
     span.done{
     color: pink;
     text-decoration: line-through;
     }
     button{
          font-family: "Delius Swash Caps", cursive;
     }
</style>
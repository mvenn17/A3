<script>
let todoItem = $state ('');
let todoList = $state ([]);

function addItem() {
     event.preventDefault();
     if (todoItem == ''){
          return;
     }
     todoList = [...todoList, {
          text: todoItem,
          done: false
     }];
     todoItem = '';
}

function removeItem(index) {
     todoList = todoList.toSpliced(index, 1);
}

function nuke (){
     todoList = [];
}

$inspect(todoList);

</script>
<form onsubmit={addItem}>
<input type="text" bind:value={todoItem}>
<button type="submit">Add</button>
</form>

<div class="listContainer">
     <ul>
          {#each todoList as item, index}
               <li>
                    <input class="checkbox" type="checkbox" bind:checked={item.done}>
                    <span class:done={item.done}>{item.text}</span>
                    <button type="button" onclick={() => removeItem(index)}>x</button>
               </li>
          {/each}
     </ul>
</div>


{#if (todoList.length == 0)}
<button disabled type="button">Clear All</button>
{:else}
<button type="button" onclick={nuke}>Clear All</button>
{/if}
<style>
.checkbox {
     background-color: #daee77;
     
     width: 1.3em;
    height: 1.3em;
    background-color: white;
    border-radius: 50%;
    vertical-align: middle;
    border: 1px solid #ddd;
    appearance: none;
    -webkit-appearance: none;
    outline: none;
    cursor: pointer;
}
.checkbox:checked {
     background-color: #91f991bb;
}

     .listContainer {

          display: flex;
          align-items: center;
          flex-direction: column;

 /*          background-color: cornsilk;
          color: black;
          margin: 2% 40% 2%;
          border-radius: 30px; */
     }
     ul{
          list-style: none;
          display: flex;
          flex-direction: column;
          align-items: flex-start;
          padding: 0px;
     }
     li{
          display: flex;
          flex-direction: row;
          justify-content: space-between;
          width: 100%;
     }
     li > span{
          flex-grow: 5;
          margin: 0px 10px;
          display: flex;
          justify-content: flex-start;
     }
     span.done {
     color: grey;
     text-decoration: line-through;
     }
</style>
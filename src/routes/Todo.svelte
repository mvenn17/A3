<script>
  import { fly } from 'svelte/transition';
  let todoItem = $state("");
  let todoList = $state([]);

  function addItem() {
    event.preventDefault();
    if (todoItem == "") {
      return;
    }
    todoList = [
      ...todoList,
      {
        text: todoItem,
        done: false,
      },
    ];
    todoItem = "";
  }

  function removeItem(index) {
    todoList = todoList.toSpliced(index, 1);
  }

  function nuke() {
    todoList = [];
  }

  $inspect(todoList);
</script>

<form onsubmit={addItem}>
  <input class="box" type="text" bind:value={todoItem} />
  <button class="add" type="submit">Add</button>
</form>

<div class="listContainer">
  <ul>
    {#each todoList as item, index}
      <li in:fly={{ x: -200, duration: 500}} out:fly={{ x: 200, duration: 500}}>
        <input class="checkbox" type="checkbox" bind:checked={item.done} />
        <span class:done={item.done}>{item.text}</span>
        <button class="x" type="button" onclick={() => removeItem(index)}>x</button>
      </li>
    {/each}
  </ul>
</div>

{#if todoList.length == 0}
  <button class="clear" disabled type="button">Clear All</button>
{:else}
  <button class="clear" type="button" onclick={nuke}>Clear All</button>
{/if}

<style>
  .clear {
    border-radius: 20px;
    font-size: 0.7em;
    border: 0;
    background-color: #979be3;
    font-family: "Chewy", system-ui;
    color: white;
    padding: 5px 10px;
    transition: 0.3s;
    text-shadow: 1px 1px 1px rgb(0, 0, 0);
  }
  .clear:hover {
    background-color: #535586;
    transition: 0.3s;
  }
  .clear:disabled {
    opacity: 50%;
    border-radius: 20px;
    font-size: 0.7em;
    border: 0;
    background-color: #979be3;
    font-family: "Chewy", system-ui;
    color: white;
    padding: 5px 10px;
  }
  .box {
    border-radius: 20px;
    font-size: 0.7em;
    border: 0;
    padding: 5px 10px;
  }
  .add {
    border-radius: 20px;
    font-size: 0.7em;
    border: 0;
    background-color: #979be3;
    font-family: "Chewy", system-ui;
    color: white;
    padding: 5px 10px;
    transition: 0.3s;
    text-shadow: 1px 1px 1px rgb(0, 0, 0);
  }
  .add:hover {
    background-color: #535586;
    transition: 0.3s;
  }
  .x {
    border-radius: 20px;
    font-size: 0.8em;
    border: 0;
    background-color: #979be3;
    font-family: "Chewy", system-ui;
    color: white;
    padding: 0px 10px;
    transition: 0.3s;
    text-shadow: 1px 1px 1px rgb(0, 0, 0);
  }
  .x:hover {
    background-color: #535586;
    transition: 0.3s;
  }
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
    transition: 0.2s;
  }
  .checkbox:checked {
    background-color: #91f991bb;
  }
  .listContainer {
    display: flex;
    align-items: center;
    flex-direction: column;
    font-family: "Quicksand", sans-serif;
    font-size: 0.7em;
    font-weight: 600;
  }
  ul {
    list-style: none;
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    padding: 0px;
  }
  li {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 100%;
    padding: 5px;
    text-shadow: 1px 1px 1px rgb(0, 0, 0);
  }
  li > span {
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

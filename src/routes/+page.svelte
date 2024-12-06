<script>
     import '../style.css';
     import Todo from './Todo.svelte';
     import Confetti from './Confetti.svelte';
</script>

<h1>To Do App</h1>

<Todo />

<!-- confetti -->
<div id="emitter"></div>
<!-- confetti^^ -->

<style>

     h1 {
          text-shadow: 1px 1px 2px #000000;
          font-size: 3em;
     }
     
</style>
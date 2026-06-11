<script>
  export let question;
  export let onAnswered;
  export let selectedAnswer = null;

  let selected = null;
  let disabled = false;

  import { onMount } from 'svelte';

  // On mount, if selectedAnswer exists, mark the option
  onMount(() => {
    if (selectedAnswer !== null) {
      selected = selectedAnswer;
      disabled = true;

      const listItems = document.querySelectorAll('.card-body li.option');
      const li = listItems[selectedAnswer];
      li.classList.remove('bg-light');
      if (selected === question.correct) {
        li.classList.add('bg-success', 'text-white');
      } else {
        li.classList.add('bg-danger', 'text-white');
      }
    }
  });

  function selectOption(i, event) {
    if (disabled) return;

    selected = i;
    disabled = true;
    onAnswered(i);

    event.currentTarget.classList.remove('bg-light');

    if (selected === question.correct) {
      event.currentTarget.classList.add('bg-success', 'text-white');
    } else {
      event.currentTarget.classList.add('bg-danger', 'text-white');
    }
  }
</script>

<div class="card quiz-card mx-auto shadow-sm">
  <div class="card-header p-3">{question.question}</div>

  <div class="card-body">
    <ul class="list-unstyled m-0">
      {#each question.options as option, i}
        <li
          class="option bg-light"
          class:disabled={disabled}
          on:click={(event) => selectOption(i, event)}
        >
          {option}
        </li>
      {/each}
    </ul>
  </div>
</div>

<style>
.card-header {
  font-weight: 600;
}

.option {
  margin-bottom: 6px;
  padding: 6px 12px;
  border: 1px solid rgba(0,0,0,0.1);
  border-radius: 6px;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.option:last-child { margin-bottom: 0; }

.option.disabled { pointer-events: none; }
</style>

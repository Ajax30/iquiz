<script>
  export let correctCount;
  export let totalQuestions;
  export let onTryAgain;
  let percentage = Math.round((correctCount / totalQuestions) * 100);
</script>

<div class="result my-2 text-center {percentage >= 70 ? 'bg-success text-white' : 'bg-danger text-white'}">
  <p class="m-0">Score: {correctCount}/{totalQuestions} ({percentage}%)</p>
  <p class="m-0">Result: {percentage >= 70 ? 'Passed' : 'Failed'}</p>
</div>
{#if percentage < 100}
	<div class="my-2">
		<button class="btn btn-primary btn-sm w-100" on:click={onTryAgain}>Try Again</button>
</div>
{/if}	

<style>
	.result {
    padding: 6px 12px;
    border: 1px solid rgba(0, 0, 0, 0.1);
    border-radius: 6px;
		text-align: center;
	}
</style>
<script>
  export let current;
  export let total;
  $: percent = Math.round((current / total) * 100);
</script>

<div class="progress-container mb-2 shadow-sm">
	<p class="small text-muted mb-1">Question {current} of {total}</p>
	<div class="progress mb-1">
	  <div
	    class="progress-bar"
	    role="progressbar"
	    style="width: {percent}%"
	    aria-valuenow={percent}
	    aria-valuemin="0"
	    aria-valuemax="100"
	  >
	    {percent}%
	  </div>
	</div>
</div>

<style>
	.progress-container {
		background: #fff;
		border-radius: 6px;
		padding: 6px 12px;
		border: 1px solid rgba(0,0,0,0.1);
	}
</style>

<script>
  export let prev;
  export let next;
  export let disablePrev = false;
  export let disableNext = false;
</script>

<div class="card-nav d-flex justify-content-between my-2">
  <button class="btn rounded-pill btn-sm btn-primary" on:click={prev} disabled={disablePrev}>
    Previous
  </button>

  <button class="btn rounded-pill btn-sm btn-primary" on:click={next} disabled={disableNext}>
    Next
  </button>
</div>

<style>
	.card-nav .btn {
		width: 45%;
		max-width: 90px;
	}
</style>
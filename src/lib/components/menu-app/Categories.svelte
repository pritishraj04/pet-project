<script>
  export let categories, classes, filterItems;
</script>

<section class="sec-gap">
  <ul class="menu-tabs">
    {#each categories as category}
      <li>
        <button
          class={classes === category ? "active" : ""}
          on:click={() => filterItems(category)}>{category}</button
        >
      </li>
    {/each}
  </ul>
</section>

<style>
  .menu-tabs {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
  }
  .active {
    background: var(--clr-primary-1);
    color: var(--clr-grey-10);
  }
</style>

<script>
  let project = "Pet Project";
</script>

<header>
  <div class="container">
    <div class="bar">
      <div class="l-corner"><h3>{project}</h3></div>
      <div class="r-corner">
        <ul class="nav-links">
          <li class="link"><a href="/">Home</a></li>
          <li class="link"><a href="/menu">Menu App</a></li>
        </ul>
      </div>
    </div>
  </div>
</header>

<style>
  .bar {
    border-radius: 5px;
    display: flex;
    justify-content: space-between;
    padding: 1.2rem 1.5rem;
    margin-top: 2.5rem;
    box-shadow: var(--default-shadow);
  }
  ul {
    display: flex;
    gap: 20px;
  }
</style>

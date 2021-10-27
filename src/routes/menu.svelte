<script>
  import Categories from "$lib/components/menu-app/Categories.svelte";
  import Menu from "$lib/components/menu-app/Menu.svelte";
  import menus from "$lib/data-center/menu-data";
  const allCategories = ["all", ...new Set(menus.map((item) => item.category))];
  let categories = allCategories;
  let menuItems = menus;
  let selectedCategory = "all";
  const filterItems = (category) => {
    if (category === "all") {
      menuItems = menus;
      selectedCategory = "all";
      return;
    }
    const newItems = menus.filter((item) => item.category === category);
    menuItems = newItems;
    selectedCategory = category;
  };
</script>

<div class="container">
  <section class="sec-gap">
    <div class="title">
      <h4>Welcome to Menu App</h4>
      <div class="underline" />
      <div class="app-window">
        <Categories classes={selectedCategory} {categories} {filterItems} />
        <Menu items={menuItems} />
      </div>
    </div>
  </section>
</div>

<style>
  .underline {
    background: var(--clr-primary-1);
    width: 5rem;
    height: 0.29rem;
    margin-right: auto;
    margin-left: auto;
    margin-top: 0.6rem;
  }
  h4 {
    text-align: center;
  }
</style>

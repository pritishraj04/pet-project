<script>
  import { total } from "$lib/data-center/stores";
  import { fly, blur, scale } from "svelte/transition";
  let subTotal;
  let isVisible = true;
  let isDetail = false;
  total.subscribe((value) => {
    subTotal = value;
  });
  export let items;

  function roundToTwo(num) {
    return +(Math.round(num + "e+2") + "e-2");
  }
</script>

{#if subTotal != 0}
  <div in:fly out:fly class={isVisible ? "bag-cal" : "bag-cal bag-hidden"}>
    <div class={isDetail ? "item-detail" : "detail-hide item-detail"}>
      <h4>Items Selected:</h4>
      <ul>
        {#each items as item}
          {#if item.count >= 1}
            <li in:blur out:blur>
              <h5>{item.count >= 1 ? item.title : ""}</h5>
              <p>{item.count >= 1 ? "× " + item.count : ""}</p>
              <h5>
                {item.count >= 1
                  ? "= ₹" + roundToTwo((item.total = item.price * item.count))
                  : ""}
              </h5>
            </li>
          {/if}
        {/each}
      </ul>
    </div>
    <div class="total">
      <h5>Total value in bag: ₹{subTotal}</h5>
      <h6>GST: +5%</h6>
      <h6>Service Tax: +2%</h6>
      <h4 class="highlight-default">
        Amount to be Paid: ₹{Math.round(subTotal + subTotal * (0.05 + 0.02))}*
      </h4>
    </div>
    <div class="disc">
      <p>*This amount is rounded off to the nearest integer.</p>
      <p>*This amount is GST included.</p>
    </div>
    <button
      class="hide-toggler"
      on:click={() => {
        isVisible = !isVisible;
        isDetail = false;
      }}>{isVisible ? "⟫" : "⟪"}</button
    >
    <button
      title="Details"
      class="detail-toggler"
      on:click={() => (isDetail = !isDetail)}
      ><span style={isDetail ? "transform: rotate(-90deg)" : ""}>⟫</span
      ></button
    >
  </div>
  <!-- ▶◀≪≫ ⟫⟪  ∧∨⨇⨈⩓⩖⩕⩔-->
{/if}
<section class="sec-gap">
  <div class="menus">
    {#each items as item}
      <article in:scale out:scale class="menu-item">
        <img src={item.img} alt={item.title} class="photo" />
        <div class="item-info">
          <header>
            <h4>{item.title}</h4>
            <h4 class="price">₹{item.price}</h4>
          </header>
          <p class="item-text">{item.desc}</p>
        </div>
        <div class="item-control">
          {#if item.count === 0}
            <button disabled class="control">-</button>
          {:else}
            <button
              on:click={() => {
                item.count -= 1;
                total.update((n) => roundToTwo(n - item.price));
              }}
              class="control">-</button
            >
          {/if}
          <p class="count">{item.count}</p>
          <button
            on:click={() => {
              item.count += 1;
              total.update((n) => roundToTwo(n + item.price));
            }}
            class="control">+</button
          >
          <!-- <div class="item-total">
            <h5>
              Item Total: ₹{roundToTwo((item.total = item.price * item.count))}
            </h5>
          </div> -->
        </div>
      </article>
    {:else}
      <h4 style="text-align: center; grid-column-start: 1; grid-column-end: 5;">
        Something Went Wrong. Please refresh the page.
      </h4>
    {/each}
  </div>
</section>

<style>
  .menus {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    justify-items: center;
    gap: 1.5rem;
    overflow: hidden;
  }
  .menu-item {
    max-width: 450px;
    border-radius: 5px;
    background: var(--clr-grey-10);
  }
  .photo {
    width: 100%;
    height: 200px;
    object-fit: cover;
    border-radius: 5px;
  }
  .item-info {
    padding: 1rem;
  }
  .item-control {
    display: flex;
    align-items: center;
    padding: 0 0 1rem 1rem;
  }
  .control {
    padding: 0.1rem 0.4rem;
    border-radius: 50%;
    margin: 0;
  }
  .count {
    font-size: 1.3rem;
    margin: 0 0.3rem;
  }
  h4,
  h5 {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
      Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
    margin-bottom: 0.3rem;
    text-transform: capitalize;
  }
  p {
    font-size: 0.9rem;
  }
  /* .item-total {
    margin-left: 0.4rem;
    padding: 0.2rem 0.32rem;
    border-radius: 5px;
    background: var(--clr-primary-9);
  } */

  .bag-cal {
    position: fixed;
    top: 25%;
    right: 1.5rem;
    padding: 1rem;
    border-radius: 5px;
    background: var(--clr-trans-white);
    backdrop-filter: blur(20px);
    -webkit-backdrop-filter: blur(20px);
    box-shadow: var(--default-shadow);
    transition: right 150ms;
    z-index: 99;
  }
  .bag-cal h4 {
    font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
    font-weight: 700;
  }
  .bag-hidden {
    right: -15rem;
  }
  .bag-cal p {
    font-size: 0.6rem;
  }
  .hide-toggler {
    position: absolute;
    left: -1.8rem;
    top: -0.1rem;
    height: 100%;
    border: none;
    cursor: pointer;
  }
  .item-detail {
    border-bottom: 0.01rem solid var(--clr-grey-8);
    padding-bottom: 1rem;
    margin-bottom: 1rem;
    transition: height 250ms, display 300ms;
  }
  .detail-hide {
    height: 0;
    display: none;
  }
  .detail-toggler {
    margin-top: 0.4rem;
    margin-bottom: -0.4rem;
    left: -0.2rem;
    width: 100%;
    border: none;
    cursor: pointer;
  }
  .detail-toggler span {
    display: inline-block;
    transform: rotate(90deg);
  }
  .item-detail h4 {
    text-align: center;
  }
  .item-detail ul {
    padding-top: 0.5rem;
    padding-right: 0.3rem;
    max-height: 15rem;
    overflow-y: auto;
  }
  /* width */
  .item-detail ul::-webkit-scrollbar {
    width: 0.3rem;
  }

  /* Track */
  .item-detail ul::-webkit-scrollbar-track {
    background: var(--clr-grey-9);
  }

  /* Handle */
  .item-detail ul::-webkit-scrollbar-thumb {
    background: var(--clr-grey-5);
  }

  /* Handle on hover */
  .item-detail ul::-webkit-scrollbar-thumb:hover {
    background: var(--clr-grey-3);
  }
  .item-detail ul li {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  li > h5:first-child:empty {
    display: none;
  }
  @media (max-width: 1200px) {
  }

  @media (max-width: 992px) {
    .menus {
      grid-template-columns: repeat(3, 1fr);
    }
  }
  @media (max-width: 768px) {
    .menus {
      grid-template-columns: repeat(2, 1fr);
    }
  }
  @media (max-width: 576px) {
    .menus {
      grid-template-columns: 1fr;
    }
    .item-detail ul {
      max-height: 12rem;
    }
  }
  @media (max-width: 320px) {
    .bag-cal {
      width: 60%; /* fallback if needed */
      width: calc(100% - 2.5em);
      top: 1rem;
      right: 0.5rem;
    }
    .bag-cal h4 {
      font-size: 0.7rem;
    }
    .bag-cal p {
      font-size: 0.5rem;
    }
    .bag-hidden {
      width: auto;
      right: -13rem;
    }
    .item-detail ul {
      max-height: 10rem;
    }
    .item-detail h5 {
      font-size: 0.7rem;
    }
  }
</style>

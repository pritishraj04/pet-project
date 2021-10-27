<script>
  let project = "Pet Project";
</script>

<footer>
  <div class="container">
    <section class="sec-gap-top">
      <div class="top">
        <h3>{project}</h3>
      </div>
      <div class="middle">
        <div class="footer-nav">
          <div class="l-f-nav">
            <h4>Pages</h4>
            <ul>
              <li><a href="/">Home</a></li>
              <li><a href="/menu">Menu App</a></li>
            </ul>
          </div>
          <div class="m-f-nav">
            <h4>Links</h4>
            <ul>
              <li>
                <a
                  href="https://pritishraj04.github.io/frontent-mentor-card-purple/"
                  target="”_blank”">Frontend Mentor Challenge</a
                >
              </li>
              <li>
                <a
                  href="https://pritishraj04.github.io/frontent-homepage-responsive/"
                  target="”_blank”">Responsive Frontend Website</a
                >
              </li>
              <li>
                <a
                  href="https://pritishraj04.github.io/react-menu/"
                  target="”_blank”">React Menu App</a
                >
              </li>
              <li>
                <a
                  href="https://pritishraj04.github.io/google-clone/"
                  target="”_blank”">Google's Clone</a
                >
              </li>
              <li>
                <a
                  href="https://pritishraj04.github.io/polardot/"
                  target="”_blank”">React Base App</a
                >
              </li>
            </ul>
          </div>
          <div class="r-f-nav">
            <h4>Subscribe to News Letter</h4>
            <form>
              <input type="text" placeholder="Enter Email" /><button
                type="submit">Submit</button
              >
            </form>
          </div>
        </div>
      </div>
      <div class="bottom">
        <p>
          Pet Project 🤑 2021 | All Rights NOT Reserved | Made by Pritish Raj
        </p>
      </div>
    </section>
  </div>
</footer>

<style>
  footer {
    background: var(--clr-grey-1);
    color: var(--clr-grey-5);
  }
  h3,
  h4 {
    color: var(--clr-grey-7);
  }
  li a {
    color: var(--clr-grey-5);
    margin-bottom: 0.5rem;
  }
  li a:hover {
    color: var(--clr-primary-10);
  }
  .footer-nav {
    display: grid;
    grid-template-columns: 1fr 1fr 2fr;
    gap: 20px;
  }
  input {
    width: 40%;
    min-width: 10rem;
  }
  @media (max-width: 768px) {
    .footer-nav {
      grid-template-columns: 1fr;
    }
  }
  .top,
  .middle,
  .bottom {
    padding: 1.2rem 0;
  }
  .top h3 {
    font-weight: 900;
  }
  .middle h4 {
    margin-bottom: 0.5rem;
    font-size: 1.2rem;
  }
  .bottom p {
    color: var(--clr-grey-7);
    text-align: center;
    font-size: 0.7rem;
  }
</style>

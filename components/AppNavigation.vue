<template>
  <nav class="app-nav">
    <ul class="app-nav-links">
      <li>
        <nuxt-link to="/" class="app-nav-link">Luiza Benisano</nuxt-link>
      </li>
    </ul>
  </nav>
</template>

<script>
export default {}
</script>

<style>
.app-nav {
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 2.4rem 0;
  color: var(--clr-light);
  background-color: var(--clr-primary-1);
}

.app-nav-links {
  display: flex;
  align-items: center;
  padding: 0 1rem;
  width: 100%;
  max-width: 129.6rem;
}

.app-nav-link {
  font-size: 1.8rem;
  font-weight: var(--fw-bold);
}

.app-nav-link:nth-child(1) {
  font-size: 2.4rem;
  font-family: var(--ff-header);
}
</style>

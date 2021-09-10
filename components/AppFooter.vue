<template>
  <footer class="app-footer">
    <ul>
      <li class="link"><nuxt-link to="/">HOME</nuxt-link></li>
    </ul>
  </footer>
</template>
<style>
.app-footer {
  display: flex;
  align-items: center;
  height: 15rem;
  width: 100%;
  padding: 2.4rem 3.6rem;
  background-color: var(--clr-primary-1);
}

.app-footer .link {
  font-weight: var(--fw-bold);
}

.app-footer .link:hover {
  color: var(--clr-accent);
}
</style>

<template>
  <header class="page-header">
    <div class="logo">
      <nuxt-link :to="'/'">
        <svg
          viewBox="0 0 368 269"
          xmlns="http://www.w3.org/2000/svg"
          fill-rule="evenodd"
          clip-rule="evenodd"
          stroke-linejoin="round"
          stroke-miterlimit="1.414"
        >
          <path d="M268.701 0l98.995 98.994-70.71 70.711-14.143-14.142-28.284 28.284 14.142 14.142-70.71 70.711-98.996-98.995L268.701-.001zm-70.71 127.279l-42.427 42.426 42.426 42.426 42.427-42.426-42.427-42.426zm113.137-28.285L268.7 56.568l-42.426 42.426 42.426 42.427 42.427-42.427z" fill="#2b2636" />
          <path d="M0 98.995L98.995 0l169.706 169.706-28.284 28.284-70.711-70.71-42.426 42.426 70.71 70.71-28.284 28.285L0 98.995zm98.995-42.427L56.57 98.995l42.426 42.426 42.427-42.426-42.427-42.427z" fill="orange" fill-opacity=".8" />
        </svg>
      </nuxt-link>
    </div>
    <div>
      <nuxt-link :to="'/'">
        Alex Benz - frontend meetup - headless CMS - nuxt.js
      </nuxt-link>
    </div>
  </header>
</template>

<script>
export default {
  name: 'PageHeader'
}
</script>

<style lang="scss" scoped>
  .page-header {
    position: fixed;
    top: 0;
    width: 100%;
    padding: 10px 50px;
    height: 60px;
    display: flex;
    align-items: center;
    background: rgba(255,255,255,0.85);

    a {
      color: black;
      text-decoration: none;
    }
  }

  .logo {
    width: 100px;
    svg {
      width: 100%;
      height: 100%;

      max-width: 100px;
      max-height: 50px;
    }
  }
</style>

<template>
  <footer class="page-footer">
    <p>
      alexander benz - komturstr. 41a - 79106 freiburg
    </p>
    <p>
      phone: <a href="tel:+49 176 434 959 54">+49 176 434 959 54</a> - mail: <a href="mailto:web@alex-benz.de">web@alex-benz.de</a>
    </p>
  </footer>
</template>

<script>
export default {
  name: 'PageFooter'
}
</script>

<style lang="scss" scoped>
  .page-footer {
    position: fixed;
    bottom: 0;
    width: 100%;
    background: #f2f2f2;
    padding: 5px 50px;

    p {
      margin: 5px 0;
    }
  }
</style>

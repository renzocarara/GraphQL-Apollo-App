<template>
  <div class="container-fluid my-footer">
      <span>
            <a
                class="my-link"
                href="https://www.renzocarara.it/"
                target="_blank"
                rel="noopener noreferrer"
                >Renzo Carara - &copy; {{ new Date().getFullYear() }}
            </a>
      </span>
  </div>
</template>

<style lang="css" scoped>
.my-footer {
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
    color: white;
    background-color: gray;
    text-align: center;
}
.my-link {
    text-decoration: none;
    color: white;
}
</style>

<template>
  <div class="leftContainer">
    <div class="logo">
      <a href="/">
        <img src="/logo.svg" alt="Logo" />
      </a>
    </div>
    
    <div class="content">
      <img src="../assets/heroImage.svg" class="heroImage" alt="Hero Image" />
      <p class="title">Team Achieve</p>
      <p class="subtitle">Your perfect solution for funding your desires</p>
    </div>
  </div>
</template>

<style lang="scss" scoped>
  .leftContainer {
    padding: var(--padding-2);
    height: 100vh;

    .logo {
      height: fit-content;
      margin-left: var(--margin-1);
    }

    .content {
      margin-top: var(--margin-2);
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: var(--gap-1_5);
      font-weight: var(--font-700);
      font-family: 'Lora', sans-serif;

      .title {
        font-size: var(--font-20);
        color: var(--color-primary);
      }

      .subtitle {
        font-size: var(--font-18);
        color: var(--color-gray-1);
      }
    }
  }

  @media screen and (width < 1024px) {
    .leftContainer {
      text-align: center;
      height: fit-content;

      .content {
        display: none;
      }
    }
  }
</style>
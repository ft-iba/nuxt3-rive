<script setup lang="ts">
</script>

<template>
  <p class="toGithub">
    <a
      href="https://github.com/ft-iba/nuxt3-rive"
      class="toGithub__link"
      target="_blank"
    >
      <span class="toGithub__label">github</span>
      <span class="toGithub__icon">
        <svg width="12" height="12" viewBox="0 0 12 12" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path fill-rule="evenodd" clip-rule="evenodd" d="M0.5 1.25C0.5 0.835786 0.835786 0.5 1.25 0.5H5V1.5H1.5V10.5H10.5V7H11.5V10.75C11.5 11.1642 11.1642 11.5 10.75 11.5H1.25C0.835787 11.5 0.5 11.1642 0.5 10.75V1.25Z" />
          <path fill-rule="evenodd" clip-rule="evenodd" d="M11.5 4L10.5 4L10.5 1.5L8 1.5L8 0.499999L11.5 0.5L11.5 4Z" />
          <path fill-rule="evenodd" clip-rule="evenodd" d="M6.30423 4.89108L10.5469 0.648438L11.254 1.35554L7.01134 5.59818L6.30423 4.89108Z" />
        </svg>
      </span>
    </a>
  </p>
</template>

<style>
.toGithub {
  padding-top: 1rem;
  padding-bottom: 1rem;
  text-align: center;
}

.toGithub__link {
  display: flex;
  align-items: baseline;
  justify-content: center;
  font-size: 1rem;
}

.toGithub__icon {
  width: 1.2rem;
}

.toGithub__icon svg {
  aspect-ratio: 1;
  width: 100%;
}

.toGithub__icon path {
  fill: currentColor;
}
</style>

<script setup></script>

<template>
  <button class="button">
    <div>
      <slot name="icon" />
    </div>
    <slot />
  </button>
</template>

<style scoped>
.button {
  border: none;
  border-radius: 10px;
  background: var(--gradient);
  padding: 14px;
  font-family: var(--font);
  font-size: 20px;
  font-weight: 600;
  color: var(--primary);
  cursor: pointer;
  height: 53px;
  width: 100%;
  display: flex;
  width: 100%;
  gap: 9px;
  align-items: center;
  justify-content: center;
}
.button:hover {
  background: var(--gradient-inverted);
  transition: background 0.3s ease-in-out;
}
</style>

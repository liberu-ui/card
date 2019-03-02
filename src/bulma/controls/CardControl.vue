<template>
    <a class="card-header-icon"
        v-on="$listeners">
        <slot/>
    </a>
</template>

export default {
  name: 'CardControl',
}

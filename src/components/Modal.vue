<template>
  <transition :duration="{leave: 200}">
  <div v-show="showing" class="fixed z-10 inset-0 overflow-y-auto">
    <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
      <transition
        enter-active-class="ease-out duration-300"
        enter-from-class="opacity-0"
        enter-to-class="opacity-100"
        leave-active-class="ease-in duration-200"
        leave-from-class="opacity-100"
        leave-to-class="opacity-0"
      >
        <div
          v-show="showing"
          class="fixed inset-0 transition-opacity"
          @click="$emit('close')"
        >
          <div class="absolute inset-0 bg-black opacity-70"></div>
        </div>
      </transition>
      <span class="hidden sm:inline-block sm:align-middle sm:h-screen"></span>&#8203;
      <transition
        enter-active-class="ease-out duration-300"
        enter-from-class="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
        enter-to-class="opacity-100 translate-y-0 sm:scale-100"
        leave-active-class="ease-in duration-200"
        leave-from-class="opacity-100 translate-y-0 sm:scale-100"
        leave-to-class="opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"

        @before-enter="beforeEnter"
        @enter="duringEnter"
        @after-enter="afterEnter"
      >
        <div 
          v-show="showing"
          class="w-full bg-teal-900 rounded p-4 inline-block align-bottom text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg" 
          role="dialog" 
          aria-modal="true" 
          aria-labelledby="modal-headline"
        >
          <div class="flex justify-between">
            <h1 class="text-2xl"><slot name="title"></slot></h1>
            <div class="p-3">
              <font-awesome-icon @click="$emit('close')" icon="times" class="text-white" />
            </div>
          </div>
          <slot />
        </div>
      </transition>
    </div>
  </div>
  </transition>
</template>

<script>
export default {
  props: {
    showing: {
      type: Boolean,
      default: false
    }
  },

  methods: {
    beforeEnter: function() {
      this.$emit('before-modal-open')
    },

    duringEnter: function() {
      this.$emit('during-modal-open')
    },

    afterEnter: function() {
      this.$emit('after-modal-open')
    }
  }
}
</script>
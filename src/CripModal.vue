<template>
  <div class="modal fade">
    <div class="modal-dialog" :class="sizeClass">
      <div class="modal-content">
        <div class="modal-header">
          <button type="button" class="close" data-dismiss="modal">&times;</button>
          <h4 class="modal-title">
            <slot name="title"></slot>
          </h4>
        </div><!-- /.modal-header -->
        <slot></slot>
      </div><!-- /.modal-content -->
    </div><!-- /.modal-dialog -->
  </div><!-- /.modal -->
</template>

<script>
  export default {
    props: {
      /**
       * The size of modal component.
       * @type {{type: String, default: (function(): string)}}
       */
      size: {type: String, 'default': () => ''},
      /**
       * Unique identifier of teh modal.
       * @type {{type: String, default: (function(): string)}}
       */
      id: {type: String, 'default': () => `modal-${Date.now() * Math.random()}`},
      /**
       * Property to force model close on change.
       * @type {{type: Boolean, default: (function(): boolean)}}
       */
      close: {type: Boolean, 'default': () => false}
    },

    mounted () {
      this.$emit('mounted', this.id)
      this.jqEl = $(this.$el)

      this.jqEl.on('hidden.bs.modal', e => {
        this.$emit('hidden', e)
      })

      this.jqEl.on('shown.bs.modal', () => {
        this.$emit('shown')
      })

      if (!this.close) {
        this.openModal()
      }
    },

    computed: {
      /**
       * Calculate modal size class.
       * @return {*}
       */
      sizeClass () {
        if (this.size) {
          return [`modal-${this.size}`]
        }
        return {}
      }
    },

    data () {
      return {
        jqEl: null
      }
    },

    methods: {
      /**
       * Hide modal
       */
      closeModal () {
        this.jqEl.find('button.close').trigger('click')
      },

      /**
       * Show Modal
       */
      openModal () {
        // show modal on mount
        this.jqEl.modal('show')
      }
    },

    destroyed () {
      this.$emit('destroyed', this.id)
      // Ensure that there is no backdrops when leaving this component without
      // close action (usually may happen in SPA).
      $('.modal-backdrop').remove()
    },

    watch: {
      'close' (val) {
        val ? this.closeModal() : this.openModal()
      }
    }
  }
</script>

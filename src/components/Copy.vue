<template>
  <div class="copy position-absolute" style="top: 0; right: 0;">
    <button
      name="copyRawButton"
      class="btn btn-outline-secondary bg-light btn-sm m-2"
      :class="copied ? 'd-none' : 'd-block'"
      @click="copyRaw"
    >
      <i class="far fa-clipboard fa-fw"></i>
    </button>
    <button
      class="btn btn-outline-secondary bg-light btn-sm m-2"
      :class="copied ? 'd-block' : 'd-none'"
      @click="copyRaw"
      v-tippy="{ placement: 'left', arrow: true }"
      content="copied"
    >
      <i class="fa fa-check fa-fw text-success"></i>
    </button>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import useClipboard from 'vue-clipboard3';

@Component({})
export default class Copy extends Vue {
  @Prop(String) private content!: string;
  private copied: boolean = false;

  private copyRaw() {
    const { toClipboard } = useClipboard();
    toClipboard(this.content);
    this.copied = true;
    window.setTimeout(() => {
      this.copied = false;
    }, 2000);
  }
}
</script>

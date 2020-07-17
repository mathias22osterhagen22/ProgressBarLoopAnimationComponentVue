# ProgressBarLoopAnimationComponentVue
This is a simple progress bar looping an animation where the duration can be pass ass parameter of the component

### Just copy pastle it: (height is in rem)
```html
<AutoLoopProgressBar :height="0.25" :animationDuration="refreshTime"></AutoLoopProgressBar>
```
### Component
```html
<template>
  <div class="progress" :style="`height: ${height}rem;`">
    <div
      :class="'progress-bar bg-success ' + 'progressAnimation'"
      role="progressbar"
      :style="`width: ${progressValue}%; --animationDuration: ${animationDurationStr};`"
      :aria-valuenow="`${progressValue}`"
      aria-valuemin="0"
      aria-valuemax="100"
    ></div>
  </div>
</template>

<script scoped>
  
export default {
  props: {
    animationDuration: { type: Number, default: 140 },
    height: { type: Number, default: 0.25 }
  },
  created: function() {
    console.log("------------ AutoLoopProgressBar -----------");
    console.log(
      "autoloopprogressbar",
      "Set animation duration to " + this.animationDurationStr
    );
  },
  mounted: function() {
    this.init();
  },
  data: function() {
    return {
      animationDurationData: this.animationDuration,
      progressValue: 0,
      interval: -1
    };
  },
  computed: {
    animationDurationStr: function() {
      return this.animationDurationData + ".0s";
    }
  },
  methods: {
    init: function() {
      console.log("autoloopprogressbar", "Setup timer");
      clearInterval(this.interval);
      this.interval = setInterval(() => {
        this.reset();
      }, this.animationDurationData * 1000);
      this.reset();
    },
    reset: function() {
      let tmp = this.animationDurationData;
      this.animationDurationData = 0;
      this.progressValue = 0;
      setTimeout(() => {
        this.animationDurationData = tmp;
        this.progressValue = 100;
      }, 0);
    }
  },
  watch: {
    animationDuration: function(newVar, oldVar) {
      this.animationDurationData = newVar;
      this.init();
    }
  }
};
</script>

<style scoped>
.progressAnimation {
  --animationDuration: 1s;
  -webkit-transition: var(--animationDuration) linear !important;
  -moz-transition: var(--animationDuration) linear !important;
  -o-transition: var(--animationDuration) linear !important;
  transition: var(--animationDuration) linear !important;
}
</style>
```

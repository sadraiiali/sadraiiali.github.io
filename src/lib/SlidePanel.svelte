<script>
  import { Motion, useTransform, useMotionValue } from "svelte-motion";

  const x = useMotionValue(0);
  const input = [-200, 0, 200];
  const opacity = useTransform(x, (v) => 200 / Math.sqrt(v * v));
  const output = [60, 0, 60];
</script>

<div class="bg">
  <div class="nothing-container">
    <div class="nothing">Nothing to see here</div>
  </div>
  <Motion
    drag="x"
    dragConstraints={{ left: 0, right: 0 }}
    style={{ x, opacity }}
    let:motion
  >
    <div class="inside" use:motion>
      <slot name="content" />
    </div>
  </Motion>
</div>

<style>
  .bg {
    
    @apply h-full w-full bg-black relative;
  }
  .inside {
    touch-action: none;

    @apply h-full w-full shadow-lg bg-gray-100;
  }
  .nothing-container {
    position: absolute;
    bottom: calc(50% - 100px);
    left: -50vh;
    height: 200px;
    width: 100vh;
    display: flex;
    flex-direction: row;
    align-items: flex-start;
    justify-content: center;
    color: white;
    transform: rotate(-90deg) translateY(50%);
  }
  .nothing {
    width: 100vh;
    display: flex;
    flex-direction: row;
    font-size: 4vh;
  }
</style>

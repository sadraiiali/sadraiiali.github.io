<script>
  import { Motion, useMotionValue, useMotionTemplate } from "svelte-motion";
  import { onMount, onDestroy } from "svelte";

  const x = useMotionValue(0);
  const y = useMotionValue(0);
  const shadow = useMotionTemplate`drop-shadow(${x}px ${y}px 20px rgba(200,200,0,0.85))`;

  let names = ["علیرضا صدرایی راد", "Alireza SadraiiRad"];

  let name = names[0];
  let intervalId;

  onMount(() => {
    let index = 0;
    intervalId = setInterval(() => {
      name = names[index % names.length];
      index++;
    }, 60000); // Change every 2 seconds
  });

  onDestroy(() => {
    clearInterval(intervalId);
  });

  const changeName = () => {
    name = names[(names.indexOf(name) + 1) % names.length];
  };
</script>

<Motion
  drag
  dragConstraints={{ left: 0, right: 0, top: 0, bottom: 0 }}
  style={{ x, y, filter: shadow }}
  let:motion
>
  <div
    use:motion
    style="cursor:grab;"
    on:mousedown={(e) => e.preventDefault()}
    on:click={changeName}
  >
    <h1>{name}</h1>
  </div>
</Motion>

<style>
  h1 {
    @apply text-2xl py-2 font-bold text-center border-2 border-gray-500 text-gray-600;
  }
</style>

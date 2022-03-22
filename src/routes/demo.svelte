<script>
  let rect, group;

  $: rect && console.error(group.getBBox());
  $: rect && setAttr(group.getBBox()); // This won't work

  // The following hack with setTimeout makes things work
  //$: rect && setTimeout(() => setAttr(group.getBBox()), 100)
  const setAttr = box => {
    ["x", "y", "width", "height"].map(attr => rect.setAttribute(attr, box[attr]));
  };
  const randInt = (min, max) => {
    min = Math.ceil(min);
    max = Math.floor(max);
    return Math.floor(Math.random() * (max - min + 1)) + min;
  };
</script>
<a href="/">Back home</a>
<svg>
  <g bind:this={group}>
    <rect bind:this={rect} fill="orange"></rect>
    <!-- Below #each block renders between 2 and 10 squares, spaced 5px -->
    {#each [...Array(randInt(2,10)).keys()] as i }
      <rect
        fill="green"
        x={i*20}
        y=20
        width=15
        height=15>
      </rect>  
    {/each}
  </g>
</svg>
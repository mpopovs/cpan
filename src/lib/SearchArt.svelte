<script>
    import {goto} from "$app/navigation";
    import Keydown from "svelte-keydown";
    import { Search } from "carbon-components-svelte";
  
  var searched = '';
  const search = () => {
  goto(`${searched}`)
  };
  </script>
  
  <section>

      <Search bind:value={searched}
      autocomplete = "on"
      placeholder = "Search art..."
      />
      <Keydown on:Enter={search}/>

  </section>
<script>
  
    import { 
      Button,
      } from "carbon-components-svelte";
    import {goto} from '$app/navigation';
    

   
  </script>
  
  
    <Button on:click={() => {goto('/')}} size="field" kind="tertiary">Back</Button>
 
  <slot></slot>
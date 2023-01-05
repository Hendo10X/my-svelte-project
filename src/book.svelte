<script>
    import { createEventDispatcher } from "svelte";
    import Button from "./button.svelte";
    export let bookTitle;
    export let bookPrice;
    export let bookDescription;
  
    const dispatch = createEventDispatcher();
  
    function purchaseBook() {
      dispatch("buy", bookTitle);
    }
  
  </script>
  
  <div>
    <h1>{bookTitle}</h1>
    <h2>{bookPrice}</h2>
    <p>{bookDescription}</p>
    <Button on:click={purchaseBook}>Buy</Button>
  </div>
  
  <style>
    div {
      margin: 1rem;
      padding: 1rem;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
    }
  
    h2 {
      font-size: 1rem;
      margin: 0.25rem 0;
      font-weight: bold;
    }
  
    p {
      margin: 0.25rem 0;
    }
  
  </style>
  
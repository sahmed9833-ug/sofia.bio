<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import { Router, link } from "svelte-routing";
  import MediaQuery from "svelte-media-query";

  const dispatch = createEventDispatcher();

  function dispatchLogoClick() {
    dispatch("logoClick");
  }
</script>

<Router>
  <MediaQuery query="(min-width: 1281px)" let:matches>
    {#if matches}
      <a href="/" use:link> <div class="desktop" /></a>
    {/if}
  </MediaQuery>

  <MediaQuery query="(min-width: 481px) and (max-width: 1280px)" let:matches>
    {#if matches}
      <a href="/" use:link> <div class="tablet" /></a>
    {/if}
  </MediaQuery>

  <MediaQuery query="(max-width: 480px)" let:matches>
    {#if matches}
      <a href="/" use:link on:click={dispatchLogoClick}>
        <div class="mobile" /></a
      >
    {/if}
  </MediaQuery>
</Router>

<style lang="scss">
  @import '../styles/colours.scss';

  div {
    background-image: url("../images/big-logo.webp");
    background-size: contain;
    background-repeat: no-repeat;
    background-position: center;
    margin: auto;
    margin-top: 25px;
    transition: 0.2s ease-out;
    -webkit-filter: drop-shadow(1px 1px 0 $font-primary)
                  drop-shadow(-1px -1px 0 $font-primary);
    filter: drop-shadow(1px 1px 0 $font-primary) 
            drop-shadow(-1px -1px 0 $font-primary);
  }
  div.desktop {
    height: 200px;
    width: 200px;
  }
  div.tablet {
    height: 150px;
    width: 90%;
  }
  div.mobile {
    height: 80px;
    width: 80px;
    display: block;
    float: left;
    margin-left: 13px;
    margin-top: 11px;
  }

  div:hover,
  div:active {
    transform: scale(1.02);
  }
</style>

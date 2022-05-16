<script lang="ts">
  import { fade, fly } from "svelte/transition";

  let scoreSelected: number | undefined = undefined;

  type SurveyModalPropprops = {
    headerImagePath: string;
    footerImagePath: string;
    surveyText: string;
    onSend: () => void;
  };

  export let props: SurveyModalPropprops;
</script>

<!--Overlay Effect-->
<div
  transition:fade={{ duration: 500 }}
  class="fixed inset-0 bg-gray-600 bg-opacity-50 overflow-y-auto h-full w-full"
  on:click={props.onSend}
/>

<!-- pop-up -->
<div class="absolute flex justify-center w-full">
  <div
    transition:fly={{ y: -40, duration: 500 }}
    class="absolute sm:max-w-xl w-11/12 bg-white rounded-xl mx-auto overflow-hidden shadow-lg"
  >
    <img src={props.headerImagePath} alt="survey-header" class="w-auto" />
    <div class="sm:px-14 px-8 pt-5">
      <div class="mb-6 sm:mb-12 text-xl sm:text-2xl text-left sm:text-justify">
        {props.surveyText}
      </div>

      <span class=" text-gray-400 text-sm sm:m-2 sm:hidden">Very unlikely</span>

      <div class="grid sm:place-content-center">
        <div class="grid grid-cols-12 grid-rows-2 gap-2 sm:block w-full">
          {#each Array(11) as _, i}
            <button
              on:click={(event) =>
                (scoreSelected = Number(event.target["value"]))}
              class:selected-score={scoreSelected === i}
              class:first-button-second-row={i === 6}
              class="sm:hover:scale-105 sm:hover:bg-blue-400 sm:focus:bg-blue-500 transition ease-out duration-300 col-span-2 font-semibold text-sm text-black  bg-gray-100 border border-gray-400 box-content h-9 w-9 sm:h-10 sm:w-10 xs:h-12 xs:w-12 rounded-full sm:rounded-none -ml-px sm:last:rounded-r-md sm:first:rounded-l-md"
              value={i}
              id={`btnradio${i}`}>{i}</button
            >
          {/each}
        </div>
      </div>
      <div class=" flex justify-end sm:justify-between">
        <span class=" text-gray-400 text-sm sm:ml-2 hidden sm:block"
          >Very unlikely</span
        >
        <span class=" text-gray-400 text-sm sm:mr-2">Very likely</span>
      </div>
      <div class=" flex justify-end my-7">
        <button
          on:click={props.onSend}
          class="sm:hover:scale-105 sm:focus:bg-blue-500 bg-blue-500 transition ease-out duration-300 text-white rounded-full p-3 w-full sm:w-24"
        >
          Send
        </button>
      </div>

      <footer class="text-center text-xs text-gray-400 mb-5">
        <p class=" m-1">
          Copyright © 2020 CustomerGauge | <a
            class=" text-blue-500"
            href="https://www.customergauge.com/"
            target="_blank">Visit CustomerGauge</a
          >
        </p>
        <p class=" m-1">
          This survey is conducted on behalf of CustomerGauge by <a
            class=" text-blue-500"
            href="https://customergauge.com/"
            target="_blank">CustomerGauge</a
          >.
        </p>
      </footer>

      <div class="flex justify-end">
        <img
          class=" w-24"
          alt="customer gauge footer"
          src={props.footerImagePath}
        />
      </div>
    </div>
  </div>
</div>

<!-- </div> -->
<style lang="postcss">
  .first-button-second-row {
    @apply col-start-2;
  }

  .selected-score {
    @apply bg-blue-500 text-white border-blue-500;
  }
</style>

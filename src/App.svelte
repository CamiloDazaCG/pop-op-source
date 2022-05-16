<script lang="ts">
  import SurveyModal from "./lib/SurveyModal.svelte";
  import footerLogo from "/src/images/footer-logo.png";
  import surveyHeader from "/src/images/survey-header.png";

  let modalVisible = false;
  const toggleShowModal = () => (modalVisible = !modalVisible);
</script>

<div class="h-full font-sans">
  <div class="text-center">
    <button
      on:click={toggleShowModal}
      class=" bg-blue-500 text-white rounded-md px-6 py-2 m-3"
    >
      Launch demo pop-up
    </button>
  </div>
  {#if modalVisible}
    <SurveyModal
      props={{
        headerImagePath: surveyHeader,
        footerImagePath: footerLogo,
        surveyText:
          "Based in your overall experience with us, how likely are you to recommend us to a friend or colleague?",
        onSend: toggleShowModal,
      }}
    />
  {/if}
</div>

<style lang="postcss">
  @tailwind base;
  @tailwind components;
  @tailwind utilities;
</style>

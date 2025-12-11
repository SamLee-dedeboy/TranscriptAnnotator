<script lang="ts">
  import { type Transcript } from "../constants.js";

  type Props = {
    transcripts: Transcript[];
    onTranscriptSelect: (transcript: Transcript) => Promise<void>;
  };

  let { transcripts, onTranscriptSelect }: Props = $props();

  let selectedTranscript = $state<string | null>(null);

  async function handleTranscriptClick(transcript: Transcript) {
    selectedTranscript = transcript.filename;
    await onTranscriptSelect(transcript);
  }
</script>

<div class="left-sidebar sidebar">
  <h2>Transcripts</h2>
  <ul class="transcript-list">
    {#each [...transcripts].sort( (a, b) => a.filename.localeCompare(b.filename) ) as transcript}
      <li
        class="transcript-item"
        class:active={selectedTranscript === transcript.filename}
      >
        <button
          type="button"
          class="transcript-button"
          onclick={() => handleTranscriptClick(transcript)}
        >
          {transcript.filename.replace(".txt", "")}
        </button>
      </li>
    {/each}
    {#if transcripts.length === 0}
      <li class="error">No transcripts found</li>
    {/if}
  </ul>
</div>

<style>
  .sidebar {
    background-color: #2c3e50;
    color: white;
    padding: 20px;
    overflow-y: auto;
  }

  .left-sidebar {
    width: 400px;
    border-right: 2px solid #34495e;
    position: relative;
  }

  .sidebar h2 {
    margin-bottom: 20px;
    font-size: 18px;
    border-bottom: 2px solid #34495e;
    padding-bottom: 10px;
  }

  .transcript-list {
    list-style: none;
    margin-bottom: 30px;
  }

  .transcript-item {
    margin: 5px 0;
    border-radius: 5px;
  }

  .transcript-button {
    width: 100%;
    padding: 12px;
    background-color: #34495e;
    border: none;
    border-radius: 5px;
    color: white;
    font-family: inherit;
    font-size: inherit;
    transition: background-color 0.3s;
    cursor: pointer;
    text-align: left;
  }

  .transcript-button:hover {
    background-color: #4a5f7a;
  }

  .transcript-item.active .transcript-button {
    background-color: #3498db;
  }

  .error {
    color: #e74c3c;
    font-style: italic;
    padding: 12px;
  }
</style>

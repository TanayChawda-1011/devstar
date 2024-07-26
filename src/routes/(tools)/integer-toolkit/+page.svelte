<script lang="ts">
  import { onMount } from "svelte";

  let inputText = "";
  let resultText = "";
  let incrementValue = 0;
  let incrementType = "add";

  function generateResult() {
    resultText = incrementValues(inputText, incrementValue, incrementType);
  }

  function incrementValues(input, increment, type) {
    return input
      .split(/\s+/)
      .map((str) => {
        let num = parseFloat(str);
        if (isNaN(num)) return str;
        switch (type) {
          case "add":
            return (num + increment).toString();
          case "subtract":
            return (num - increment).toString();
          case "multiply":
            return (num * increment).toString();
          case "divide":
            return increment !== 0 ? (num / increment).toString() : "Error: Division by zero";
          case "power":
            return Math.pow(num, increment).toString();
          case "root":
            return Math.pow(num, 1 / increment).toString();
          default:
            return str;
        }
      })
      .join(" ");
  }

  $: if (inputText || incrementValue !== undefined || incrementType) generateResult();
</script>

<div class="tools-container space-y-8">
  <div class="tool">
    <h1 class="text-gray-900 text-2xl dark:text-white ml-12 font-medium">
      Advanced Value Incrementor
    </h1>
    <div class="py-8 px-4 mx-auto max-w-screen-xl lg:px-12">
      <div class="card p-8 relative items-center mx-auto max-w-screen-xl overflow-hidden rounded-lg bg-white dark:bg-gray-800 shadow-lg">
        <div class="mt-4 gap-4 items-center mx-auto max-w-screen-xl grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3">
          <div class="rounded-lg overflow-hidden bg-gray-50 border border-gray-300 dark:bg-gray-700 dark:border-gray-600 p-4">
            <h2 class="text-lg font-medium text-gray-700 dark:text-white mb-2">Input Values</h2>
            <textarea
              placeholder="Enter values (one per line)"
              rows="8"
              class="resize-none block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
              bind:value={inputText}
            ></textarea>
          </div>

          <div class="rounded-lg overflow-hidden bg-gray-50 border border-gray-300 dark:bg-gray-700 dark:border-gray-600 p-4">
            <h2 class="text-lg font-medium text-gray-700 dark:text-white mb-2">Increment Settings</h2>
            <input
              type="number"
              placeholder="Enter Increment Value"
              class="block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500 mb-4"
              bind:value={incrementValue}
            />
            <select
              bind:value={incrementType}
              class="block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            >
              <option value="add">Add</option>
              <option value="subtract">Subtract</option>
              <option value="multiply">Multiply</option>
              <option value="divide">Divide</option>
              <option value="power">Power</option>
              <option value="root">Root</option>
            </select>
          </div>

          <div class="rounded-lg overflow-hidden bg-gray-50 border border-gray-300 dark:bg-gray-700 dark:border-gray-600 p-4">
            <h2 class="text-lg font-medium text-gray-700 dark:text-white mb-2">Result</h2>
            <textarea
              placeholder="Result"
              rows="8"
              class="resize-none block p-2.5 w-full text-sm text-gray-900 bg-gray-50 rounded-lg border border-gray-300 focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
              bind:value={resultText}
              readonly
            ></textarea>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>

<style>
  .card h2 {
    padding: 0.5rem 0;
  }
</style>
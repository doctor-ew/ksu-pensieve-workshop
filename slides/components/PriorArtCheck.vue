<script setup>
import { ref, computed } from 'vue'
const scenario = ref('found')
const repaired = ref(false)
const cases = {
  found: { title: 'Another team recorded a relevant decision', expected: 'Found — returned with source, who recorded it, and date', passes: true },
  conflict: { title: 'Two teams recorded conflicting decisions', expected: 'Conflict flagged — both shown, not merged', passes: false },
  superseded: { title: 'The decision was later superseded', expected: 'Shown as superseded, with its replacement', passes: false },
  none: { title: 'Nothing in shared memory matches', expected: 'Nothing found in shared memory — not “no prior work exists”', passes: false },
  failed: { title: 'The lookup times out', expected: 'Unresolved — not “nothing found”', passes: false },
}
const result = computed(() => repaired.value ? cases[scenario.value].expected : 'Checked! No prior work found.')
</script>
<template>
  <div class="handoff-demo">
    <p class="fixture-label">SYNTHETIC LOCAL FIXTURE · NO NETWORK OR REAL MEMORIES</p>
    <label for="handoff-scenario">Challenge the claim</label>
    <select id="handoff-scenario" v-model="scenario">
      <option v-for="(item, key) in cases" :key="key" :value="key">{{ item.title }}</option>
    </select>
    <button @click="repaired = !repaired">{{ repaired ? 'Show incomplete version' : 'Show repaired contract' }}</button>
    <div class="demo-result" role="status" aria-live="polite">
      <strong>{{ repaired ? 'Cited, honest check' : 'Intentionally incomplete check' }}</strong>
      <p>{{ result }}</p>
    </div>
    <p class="fixture-caption">{{ repaired ? 'Expected behavior illustrated; a real check still depends on what shared memory actually holds.' : 'Which requirement did this result fail to check?' }}</p>
  </div>
</template>
<style scoped>
.fixture-label{font-size:12px!important;color:#e6bf7a}
label{display:block;margin:18px 0 8px}
select,button{font:inherit;font-size:17px;padding:12px 16px;border:1px solid #9c865e;border-radius:5px;background:#282821;color:#fff}
button{margin-left:14px;cursor:pointer;background:#614d2c}
.demo-result{margin-top:24px;padding:22px;background:#272b29;border-left:4px solid #e5b65e;min-height:115px}
.demo-result strong{font-size:17px;color:#e6bf7a}.demo-result p{font-size:22px;margin:12px 0 0}
.fixture-caption{font-size:16px!important;color:#d1c9bb}
</style>

<script setup lang="ts">
import { ref } from "vue"

const points = ref([
  [200, 150],
  [600, 150],
  [200, 650],
  [600, 650],
  [250, 400],
  [550, 400],
  [350, 200],
  [450, 200],
  [350, 600],
  [450, 600]
])
</script>

<template>
  <div class="chip-dashboard">
    <!-- 背景电路网格 -->
    <div class="circuit-background" />

    <!-- 芯片电路 -->
    <svg class="circuit-svg" viewBox="0 0 800 800">
      <rect x="320" y="320" width="160" height="160" rx="12" class="chip-core" />

      <g class="circuit-lines" stroke="#00bcd4" stroke-width="2" fill="none">
        <path class="flow-line" d="M400 100 L400 150 L200 150 L200 300 L100 300" />
        <path class="flow-line" d="M400 100 L400 150 L600 150 L600 250 L700 250" />
        <path class="flow-line" d="M400 700 L400 650 L200 650 L200 500 L100 500" />
        <path class="flow-line" d="M400 700 L400 650 L600 650 L600 550 L700 550" />

        <path class="flow-line" d="M150 400 L250 400 L250 200 L350 200" />
        <path class="flow-line" d="M650 400 L550 400 L550 200 L450 200" />
        <path class="flow-line" d="M150 400 L250 400 L250 600 L350 600" />
        <path class="flow-line" d="M650 400 L550 400 L550 600 L450 600" />
      </g>

      <g class="signal-nodes">
        <circle
          v-for="(p, i) in points"
          :key="i"
          :cx="p[0]"
          :cy="p[1]"
          r="5"
          class="signal-dot"
        />
      </g>
    </svg>

    <div class="content">
      <h1 class="title">
        芯片制造业智能数据看板
      </h1>
      <p class="subtitle">
        实时监控 · 生产分析 · KPI 指标可视化
      </p>
    </div>
  </div>
</template>

<style scoped lang="scss">
.chip-dashboard {
  width: 100%;
  height: 100vh;
  background: transparent; /* 去掉背景色 */
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  overflow: hidden;
  position: relative;
}

.circuit-background {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(0, 188, 212, 0.08) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0, 188, 212, 0.08) 1px, transparent 1px);
  background-size: 60px 60px;
  animation: gridPulse 10s ease-in-out infinite;
  z-index: 0;
}

@keyframes gridPulse {
  0%,
  100% {
    opacity: 0.3;
    transform: scale(1);
  }
  50% {
    opacity: 0.8;
    transform: scale(1.03);
  }
}

.circuit-svg {
  width: 640px;
  height: 640px;
  z-index: 1;
}

.chip-core {
  fill: #ffffff;
  stroke: #00bcd4;
  stroke-width: 3;
  filter: drop-shadow(0 0 18px rgba(0, 188, 212, 0.5));
  animation: corePulse 0.8s ease-in-out infinite;
}

@keyframes corePulse {
  0%,
  100% {
    stroke-width: 3;
    filter: drop-shadow(0 0 8px rgba(0, 188, 212, 0.4));
  }
  50% {
    stroke-width: 6;
    filter: drop-shadow(0 0 28px rgba(0, 188, 212, 1));
  }
}

.energy-ring {
  fill: none;
  stroke: rgba(0, 188, 212, 0.4);
  stroke-width: 3;
  stroke-dasharray: 12 10;
  transform-origin: center;
  animation: rotateRing 10s linear infinite;
}

@keyframes rotateRing {
  to {
    transform: rotate(360deg);
  }
}

.flow-line {
  stroke-dasharray: 250;
  stroke-dashoffset: 250;
  animation: lineFlow 8s linear infinite;
  opacity: 0.9;
}

@keyframes lineFlow {
  to {
    stroke-dashoffset: 0;
  }
}

.signal-dot {
  fill: #00eaff;
  filter: drop-shadow(0 0 10px #00eaff);
  animation: blink 1.4s ease-in-out infinite;
}

.signal-dot:nth-child(2n) {
  animation-delay: 0.3s;
}
.signal-dot:nth-child(3n) {
  animation-delay: 0.6s;
}
.signal-dot:nth-child(4n) {
  animation-delay: 0.9s;
}

@keyframes blink {
  0%,
  100% {
    opacity: 0.2;
    r: 4;
  }
  50% {
    opacity: 1;
    r: 6;
  }
}

.content {
  text-align: center;
  z-index: 3;
  margin-top: 40px;
}

.title {
  font-size: 34px;
  color: #00acc1;
  font-weight: 700;
  letter-spacing: 1.5px;
  text-shadow: 0 0 10px rgba(0, 188, 212, 0.25);
}

.subtitle {
  font-size: 16px;
  color: #007c91;
  margin-top: 10px;
  letter-spacing: 0.5px;
}

.enter-btn {
  margin-top: 30px;
  padding: 12px 40px;
  border: none;
  border-radius: 25px;
  font-size: 16px;
  color: white;
  background: linear-gradient(90deg, #00c6ff, #0072ff);
  cursor: pointer;
  box-shadow: 0 0 12px rgba(0, 188, 212, 0.4);
  transition: all 0.3s ease;
}

.enter-btn:hover {
  transform: scale(1.05);
  box-shadow: 0 0 25px rgba(0, 188, 212, 0.6);
}
</style>

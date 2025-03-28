<script setup>
import { ref, onMounted } from 'vue';

// 模拟数据
const dataInput = ref({
  textData: 85,
  imageData: 65,
  audioData: 45,
  videoData: 30
});

const computingPower = ref({
  gpuUsage: 78,
  cpuUsage: 62,
  memoryUsage: 55,
  storageUsage: 40
});

const networkStatus = ref({
  bandwidth: 82,
  latency: 25,
  reliability: 95,
  throughput: 70
});

const modelInference = ref({
  accuracy: 88,
  speed: 75,
  adaptability: 80,
  efficiency: 65
});

// 模拟日志数据
const logs = ref([
  { time: '10:05:26', type: '数据输入', message: '接收到新的文化数据包', status: '成功' },
  { time: '10:05:28', type: '算力分配', message: '为推理任务分配GPU资源', status: '成功' },
  { time: '10:05:30', type: '网络传输', message: '数据包传输至推理服务器', status: '成功' },
  { time: '10:05:32', type: '模型推理', message: '启动文化知识推理引擎', status: '进行中' },
  { time: '10:05:35', type: '模型推理', message: '生成文化元素关联图谱', status: '进行中' },
]);

// 模拟实时更新数据
let timer;
onMounted(() => {
  timer = setInterval(() => {
    // 随机更新数据
    dataInput.value.textData = updateValue(dataInput.value.textData);
    dataInput.value.imageData = updateValue(dataInput.value.imageData);
    computingPower.value.gpuUsage = updateValue(computingPower.value.gpuUsage);
    computingPower.value.cpuUsage = updateValue(computingPower.value.cpuUsage);
    networkStatus.value.bandwidth = updateValue(networkStatus.value.bandwidth);
    networkStatus.value.latency = updateValue(networkStatus.value.latency);
    modelInference.value.accuracy = updateValue(modelInference.value.accuracy);
    modelInference.value.speed = updateValue(modelInference.value.speed);
    
    // 添加新日志
    if (logs.value.length > 20) {
      logs.value.pop();
    }
    
    const now = new Date();
    const time = `${now.getHours()}:${now.getMinutes()}:${now.getSeconds()}`;
    const types = ['数据输入', '算力分配', '网络传输', '模型推理'];
    const messages = [
      '接收文化数据包',
      '分配计算资源',
      '优化网络传输',
      '执行模型推理',
      '生成文化关联',
      '更新知识图谱',
      '优化推理结果'
    ];
    const statuses = ['成功', '进行中', '等待中'];
    
    logs.value.unshift({
      time,
      type: types[Math.floor(Math.random() * types.length)],
      message: messages[Math.floor(Math.random() * messages.length)],
      status: statuses[Math.floor(Math.random() * statuses.length)]
    });
  }, 3000);
});

// 辅助函数：在一定范围内随机更新值
function updateValue(value) {
  const change = Math.random() * 10 - 5; // -5 到 5 之间的随机数
  let newValue = value + change;
  if (newValue > 100) newValue = 100;
  if (newValue < 0) newValue = 0;
  return Math.round(newValue);
}

// 根据值返回对应的颜色
function getColorByValue(value) {
  if (value >= 80) return '#42b883'; // 绿色
  if (value >= 60) return '#41b0d3'; // 蓝色
  if (value >= 40) return '#f7ba2a'; // 黄色
  return '#ff4949'; // 红色
}
</script>

<template>
  <div class="metaverse-container">
    <header class="dashboard-header">
      <h1>文化元宇宙Agent伴游系统</h1>
      <div class="system-time">{{ new Date().toLocaleString() }}</div>
    </header>
    
    <div class="dashboard-grid">
      <!-- 数据输入模块 -->
      <div class="dashboard-card">
        <div class="card-header">
          <h2>数据供给</h2>
          <div class="card-status">实时监控中</div>
        </div>
        <div class="card-content">
          <div class="gauge-container">
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${dataInput.textData * 1.8}deg)`, backgroundColor: getColorByValue(dataInput.textData)}"></div>
                <div class="gauge-center">{{ dataInput.textData }}%</div>
              </div>
              <div class="gauge-label">文本数据</div>
            </div>
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${dataInput.imageData * 1.8}deg)`, backgroundColor: getColorByValue(dataInput.imageData)}"></div>
                <div class="gauge-center">{{ dataInput.imageData }}%</div>
              </div>
              <div class="gauge-label">图像数据</div>
            </div>
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${dataInput.audioData * 1.8}deg)`, backgroundColor: getColorByValue(dataInput.audioData)}"></div>
                <div class="gauge-center">{{ dataInput.audioData }}%</div>
              </div>
              <div class="gauge-label">音频数据</div>
            </div>
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${dataInput.videoData * 1.8}deg)`, backgroundColor: getColorByValue(dataInput.videoData)}"></div>
                <div class="gauge-center">{{ dataInput.videoData }}%</div>
              </div>
              <div class="gauge-label">视频数据</div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- 算力支撑模块 -->
      <div class="dashboard-card">
        <div class="card-header">
          <h2>算力支撑</h2>
          <div class="card-status">运行正常</div>
        </div>
        <div class="card-content">
          <div class="gauge-container">
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${computingPower.gpuUsage * 1.8}deg)`, backgroundColor: getColorByValue(computingPower.gpuUsage)}"></div>
                <div class="gauge-center">{{ computingPower.gpuUsage }}%</div>
              </div>
              <div class="gauge-label">GPU使用率</div>
            </div>
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${computingPower.cpuUsage * 1.8}deg)`, backgroundColor: getColorByValue(computingPower.cpuUsage)}"></div>
                <div class="gauge-center">{{ computingPower.cpuUsage }}%</div>
              </div>
              <div class="gauge-label">CPU使用率</div>
            </div>
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${computingPower.memoryUsage * 1.8}deg)`, backgroundColor: getColorByValue(computingPower.memoryUsage)}"></div>
                <div class="gauge-center">{{ computingPower.memoryUsage }}%</div>
              </div>
              <div class="gauge-label">内存使用率</div>
            </div>
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${computingPower.storageUsage * 1.8}deg)`, backgroundColor: getColorByValue(computingPower.storageUsage)}"></div>
                <div class="gauge-center">{{ computingPower.storageUsage }}%</div>
              </div>
              <div class="gauge-label">存储使用率</div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- 网络保障模块 -->
      <div class="dashboard-card">
        <div class="card-header">
          <h2>网络保障</h2>
          <div class="card-status">连接稳定</div>
        </div>
        <div class="card-content">
          <div class="gauge-container">
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${networkStatus.bandwidth * 1.8}deg)`, backgroundColor: getColorByValue(networkStatus.bandwidth)}"></div>
                <div class="gauge-center">{{ networkStatus.bandwidth }}%</div>
              </div>
              <div class="gauge-label">带宽利用率</div>
            </div>
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${networkStatus.latency * 1.8}deg)`, backgroundColor: getColorByValue(networkStatus.latency)}"></div>
                <div class="gauge-center">{{ networkStatus.latency }}ms</div>
              </div>
              <div class="gauge-label">网络延迟</div>
            </div>
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${networkStatus.reliability * 1.8}deg)`, backgroundColor: getColorByValue(networkStatus.reliability)}"></div>
                <div class="gauge-center">{{ networkStatus.reliability }}%</div>
              </div>
              <div class="gauge-label">可靠性</div>
            </div>
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${networkStatus.throughput * 1.8}deg)`, backgroundColor: getColorByValue(networkStatus.throughput)}"></div>
                <div class="gauge-center">{{ networkStatus.throughput }}%</div>
              </div>
              <div class="gauge-label">吞吐量</div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- 模型适配模块 -->
      <div class="dashboard-card">
        <div class="card-header">
          <h2>模型适配</h2>
          <div class="card-status">推理中</div>
        </div>
        <div class="card-content">
          <div class="gauge-container">
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${modelInference.accuracy * 1.8}deg)`, backgroundColor: getColorByValue(modelInference.accuracy)}"></div>
                <div class="gauge-center">{{ modelInference.accuracy }}%</div>
              </div>
              <div class="gauge-label">推理准确率</div>
            </div>
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${modelInference.speed * 1.8}deg)`, backgroundColor: getColorByValue(modelInference.speed)}"></div>
                <div class="gauge-center">{{ modelInference.speed }}%</div>
              </div>
              <div class="gauge-label">推理速度</div>
            </div>
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${modelInference.adaptability * 1.8}deg)`, backgroundColor: getColorByValue(modelInference.adaptability)}"></div>
                <div class="gauge-center">{{ modelInference.adaptability }}%</div>
              </div>
              <div class="gauge-label">适应性</div>
            </div>
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${modelInference.efficiency * 1.8}deg)`, backgroundColor: getColorByValue(modelInference.efficiency)}"></div>
                <div class="gauge-center">{{ modelInference.efficiency }}%</div>
              </div>
              <div class="gauge-label">效率</div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- 系统日志模块 -->
      <div class="dashboard-card logs-card">
        <div class="card-header">
          <h2>系统日志</h2>
          <div class="card-status">实时更新</div>
        </div>
        <div class="card-content">
          <table class="logs-table">
            <thead>
              <tr>
                <th>时间</th>
                <th>类型</th>
                <th>消息</th>
                <th>状态</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(log, index) in logs" :key="index">
                <td>{{ log.time }}</td>
                <td>{{ log.type }}</td>
                <td>{{ log.message }}</td>
                <td :class="`status-${log.status === '成功' ? 'success' : log.status === '进行中' ? 'progress' : 'waiting'}`">{{ log.status }}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.metaverse-container {
  width: 100%;
  min-height: 100vh;
  background-color: #0a1929;
  color: #e6f7ff;
  padding: 20px;
  font-family: 'Arial', sans-serif;
}

.dashboard-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
  background-color: #001529;
  border-radius: 8px;
  margin-bottom: 20px;
  border: 1px solid #177ddc;
  box-shadow: 0 0 10px rgba(23, 125, 220, 0.5);
}

.dashboard-header h1 {
  margin: 0;
  font-size: 1.8rem;
  background: linear-gradient(90deg, #177ddc, #41b0d3);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.system-time {
  font-size: 1.2rem;
  color: #177ddc;
}

.dashboard-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: repeat(3, auto);
  gap: 20px;
}

.dashboard-card {
  background-color: #001529;
  border-radius: 8px;
  border: 1px solid #177ddc;
  box-shadow: 0 0 10px rgba(23, 125, 220, 0.3);
  overflow: hidden;
}

.logs-card {
  grid-column: span 2;
}

.card-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 15px;
  background-color: #002140;
  border-bottom: 1px solid #177ddc;
}

.card-header h2 {
  margin: 0;
  font-size: 1.2rem;
  color: #41b0d3;
}

.card-status {
  font-size: 0.9rem;
  color: #52c41a;
  background-color: rgba(82, 196, 26, 0.1);
  padding: 3px 8px;
  border-radius: 4px;
  border: 1px solid rgba(82, 196, 26, 0.2);
}

.card-content {
  padding: 15px;
}

.gauge-container {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
}

.gauge-item {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.gauge {
  position: relative;
  width: 120px;
  height: 120px;
  border-radius: 50%;
  background-color: #002140;
  overflow: hidden;
  box-shadow: 0 0 10px rgba(23, 125, 220, 0.3);
}

.gauge-fill {
  position: absolute;
  top: 0;
  left: 0;
  width: 50%;
  height: 100%;
  background-color: #42b883;
  transform-origin: right center;
  transition: transform 0.5s ease-out;
}

.gauge-center {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #001529;
  border-radius: 50%;
  transform: scale(0.85);
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 1.5rem;
  font-weight: bold;
  color: #e6f7ff;
}

.gauge-label {
  margin-top: 10px;
  font-size: 0.9rem;
  color: #8c8c8c;
}

.logs-table {
  width: 100%;
  border-collapse: collapse;
}

.logs-table th {
  background-color: #002140;
  padding: 10px;
  text-align: left;
  color: #41b0d3;
  font-weight: normal;
}

.logs-table td {
  padding: 8px 10px;
  border-bottom: 1px solid #003a6d;
}

.logs-table tr:hover {
  background-color: #002140;
}

.status-success {
  color: #52c41a;
}

.status-progress {
  color: #faad14;
}

.status-waiting {
  color: #1890ff;
}

@media (max-width: 1200px) {
  .dashboard-grid {
    grid-template-columns: 1fr;
  }
  
  .logs-card {
    grid-column: span 1;
  }
}

@media (max-width: 768px) {
  .gauge-container {
    grid-template-columns: 1fr;
  }
  
  .gauge {
    width: 100px;
    height: 100px;
  }
  
  .gauge-center {
    font-size: 1.2rem;
  }
}
</style>
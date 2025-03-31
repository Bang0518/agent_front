<script setup>
import { ref, onMounted, onUnmounted } from 'vue';
import * as echarts from 'echarts';

// 模拟数据
const systemResources = ref({
  cpuUsage: 78,
  memoryUsage: 62,
  diskUsage: 55,
  networkUsage: 40
});

const serviceStatus = ref([
  { name: '北京XX科技有限公司', cpu: 2.3, memory: 54.87, disk: 20.10, status: '正常' },
  { name: '中关村科技园区XX科技孵化器', cpu: 3.67, memory: 60.05, disk: 18.80, status: '正常' },
  { name: '经济开发区', cpu: 1.44, memory: 63.84, disk: 12.70, status: '正常' }
]);

const trafficData = ref({
  today: 231,
  yesterday: 198,
  thisWeek: 1245,
  lastWeek: 1102
});

const deviceDistribution = ref([
  { value: 40, name: '移动端' },
  { value: 30, name: '桌面端' },
  { value: 20, name: '平板' },
  { value: 10, name: '其他' }
]);

const regionDistribution = ref([
  { value: 35, name: '华北' },
  { value: 25, name: '华东' },
  { value: 20, name: '华南' },
  { value: 15, name: '西部' },
  { value: 5, name: '其他' }
]);

// 历史数据趋势
const historyTrend = ref({
  dates: ['2024-01', '2024-02', '2024-03', '2024-04', '2024-05', '2024-06'],
  values: [120, 132, 101, 134, 90, 230]
});

// 交易量数据
const transactionData = ref({
  years: ['2017', '2018', '2019', '2020', '2021', '2022', '2023', '2024'],
  values: [10, 25, 36, 42, 56, 60, 70, 65]
});

// 模拟日志数据
const logs = ref([
  { time: '10:05:26', type: '系统', message: '服务器资源监控启动', status: '成功' },
  { time: '10:05:28', type: '网络', message: '网络流量分析开始', status: '成功' },
  { time: '10:05:30', type: '安全', message: '安全扫描完成', status: '成功' },
  { time: '10:05:32', type: '服务', message: '服务健康检查', status: '进行中' },
  { time: '10:05:35', type: '数据库', message: '数据库连接池优化', status: '进行中' },
]);

// 图表实例引用
const pieChart = ref(null);
const regionChart = ref(null);
const lineChart = ref(null);
const barChart = ref(null);

// 图表DOM引用
const pieChartRef = ref(null);
const regionChartRef = ref(null);
const lineChartRef = ref(null);
const barChartRef = ref(null);

// 模拟实时更新数据
let timer;
onMounted(() => {
  // 初始化图表
  initCharts();
  
  timer = setInterval(() => {
    // 随机更新数据
    systemResources.value.cpuUsage = updateValue(systemResources.value.cpuUsage);
    systemResources.value.memoryUsage = updateValue(systemResources.value.memoryUsage);
    systemResources.value.diskUsage = updateValue(systemResources.value.diskUsage);
    systemResources.value.networkUsage = updateValue(systemResources.value.networkUsage);
    
    // 更新图表数据
    updateCharts();
    
    // 添加新日志
    if (logs.value.length > 20) {
      logs.value.pop();
    }
    
    const now = new Date();
    const time = `${now.getHours()}:${now.getMinutes()}:${now.getSeconds()}`;
    const types = ['系统', '网络', '安全', '服务', '数据库'];
    const messages = [
      '资源监控更新',
      '网络流量分析',
      '安全扫描',
      '服务健康检查',
      '数据库连接检查',
      '系统性能优化',
      '负载均衡调整'
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

onUnmounted(() => {
  clearInterval(timer);
  // 销毁图表实例
  pieChart.value && pieChart.value.dispose();
  regionChart.value && regionChart.value.dispose();
  lineChart.value && lineChart.value.dispose();
  barChart.value && barChart.value.dispose();
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

// 初始化所有图表
function initCharts() {
  // 初始化设备分布饼图
  pieChart.value = echarts.init(pieChartRef.value);
  const pieOption = {
    tooltip: {
      trigger: 'item'
    },
    legend: {
      orient: 'vertical',
      left: 'left',
      textStyle: {
        color: '#e6f7ff'
      }
    },
    series: [
      {
        name: '设备分布',
        type: 'pie',
        radius: '70%',
        data: deviceDistribution.value,
        emphasis: {
          itemStyle: {
            shadowBlur: 10,
            shadowOffsetX: 0,
            shadowColor: 'rgba(0, 0, 0, 0.5)'
          }
        },
        label: {
          color: '#e6f7ff'
        }
      }
    ],
    backgroundColor: 'transparent',
    color: ['#41b0d3', '#42b883', '#f7ba2a', '#ff4949']
  };
  pieChart.value.setOption(pieOption);
  
  // 初始化区域分布饼图
  regionChart.value = echarts.init(regionChartRef.value);
  const regionOption = {
    tooltip: {
      trigger: 'item'
    },
    legend: {
      orient: 'vertical',
      left: 'left',
      textStyle: {
        color: '#e6f7ff'
      }
    },
    series: [
      {
        name: '区域分布',
        type: 'pie',
        radius: ['40%', '70%'], // 环形图
        data: regionDistribution.value,
        emphasis: {
          itemStyle: {
            shadowBlur: 10,
            shadowOffsetX: 0,
            shadowColor: 'rgba(0, 0, 0, 0.5)'
          }
        },
        label: {
          color: '#e6f7ff'
        }
      }
    ],
    backgroundColor: 'transparent',
    color: ['#41b0d3', '#42b883', '#f7ba2a', '#ff4949', '#7265e6']
  };
  regionChart.value.setOption(regionOption);
  
  // 初始化历史趋势线图
  lineChart.value = echarts.init(lineChartRef.value);
  const lineOption = {
    tooltip: {
      trigger: 'axis'
    },
    xAxis: {
      type: 'category',
      data: historyTrend.value.dates,
      axisLine: {
        lineStyle: {
          color: '#8c8c8c'
        }
      },
      axisLabel: {
        color: '#e6f7ff'
      }
    },
    yAxis: {
      type: 'value',
      axisLine: {
        lineStyle: {
          color: '#8c8c8c'
        }
      },
      axisLabel: {
        color: '#e6f7ff'
      },
      splitLine: {
        lineStyle: {
          color: 'rgba(140, 140, 140, 0.2)'
        }
      }
    },
    series: [
      {
        data: historyTrend.value.values,
        type: 'line',
        smooth: true,
        lineStyle: {
          width: 3,
          color: '#41b0d3'
        },
        areaStyle: {
          color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
            {
              offset: 0,
              color: 'rgba(65, 176, 211, 0.5)'
            },
            {
              offset: 1,
              color: 'rgba(65, 176, 211, 0.1)'
            }
          ])
        }
      }
    ],
    backgroundColor: 'transparent'
  };
  lineChart.value.setOption(lineOption);
  
  // 初始化交易量柱状图
  barChart.value = echarts.init(barChartRef.value);
  const barOption = {
    tooltip: {
      trigger: 'axis'
    },
    xAxis: {
      type: 'category',
      data: transactionData.value.years,
      axisLine: {
        lineStyle: {
          color: '#8c8c8c'
        }
      },
      axisLabel: {
        color: '#e6f7ff'
      }
    },
    yAxis: {
      type: 'value',
      axisLine: {
        lineStyle: {
          color: '#8c8c8c'
        }
      },
      axisLabel: {
        color: '#e6f7ff'
      },
      splitLine: {
        lineStyle: {
          color: 'rgba(140, 140, 140, 0.2)'
        }
      }
    },
    series: [
      {
        data: transactionData.value.values,
        type: 'bar',
        barWidth: '40%',
        itemStyle: {
          color: new echarts.graphic.LinearGradient(0, 0, 0, 1, [
            { offset: 0, color: '#41b0d3' },
            { offset: 1, color: '#177ddc' }
          ])
        }
      }
    ],
    backgroundColor: 'transparent'
  };
  barChart.value.setOption(barOption);
}

// 更新图表数据
function updateCharts() {
  if (pieChart.value) {
    // 随机更新设备分布数据
    deviceDistribution.value.forEach(item => {
      item.value = updateValue(item.value);
    });
    pieChart.value.setOption({
      series: [{
        data: deviceDistribution.value
      }]
    });
  }
  
  if (lineChart.value) {
    // 更新最后一个数据点
    const lastIndex = historyTrend.value.values.length - 1;
    historyTrend.value.values[lastIndex] = updateValue(historyTrend.value.values[lastIndex]);
    lineChart.value.setOption({
      series: [{
        data: historyTrend.value.values
      }]
    });
  }
}
</script>

<template>
  <div class="metaverse-container">
    <header class="dashboard-header">
      <h1>XX监控系统</h1>
      <div class="system-time">{{ new Date().toLocaleString() }}</div>
    </header>
    
    <div class="dashboard-grid">
      <!-- 系统资源模块 -->
      <div class="dashboard-card">
        <div class="card-header">
          <h2>系统资源</h2>
          <div class="card-status">实时监控中</div>
        </div>
        <div class="card-content">
          <div class="gauge-container">
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${systemResources.cpuUsage * 1.8}deg)`, backgroundColor: getColorByValue(systemResources.cpuUsage)}"></div>
                <div class="gauge-center">{{ systemResources.cpuUsage }}%</div>
              </div>
              <div class="gauge-label">CPU使用率</div>
            </div>
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${systemResources.memoryUsage * 1.8}deg)`, backgroundColor: getColorByValue(systemResources.memoryUsage)}"></div>
                <div class="gauge-center">{{ systemResources.memoryUsage }}%</div>
              </div>
              <div class="gauge-label">内存使用率</div>
            </div>
            <div class="gauge-item">
              <div class="gauge">
                <div class="gauge-fill" :style="{transform: `rotate(${systemResources.diskUsage * 1.8}deg)`, backgroundColor: getColorByValue(systemResources.diskUsage)}"></div>
                <div class="gauge-center">{{ systemResources.diskUsage }}%</div>
              </div>
              <div class="gauge-label">磁盘使用率</div>
            </div>
      
              <div class="gauge-item">
                <div class="gauge">
                  <div class="gauge-fill" :style="{transform: `rotate(${systemResources.networkUsage * 1.8}deg)`, backgroundColor: getColorByValue(systemResources.networkUsage)}"></div>
                  <div class="gauge-center">{{ systemResources.networkUsage }}%</div>
                </div>
                <div class="gauge-label">网络使用率</div>
              </div>
            </div>
          </div>
        </div>
        
        <!-- 服务状态模块 -->
        <div class="dashboard-card">
          <div class="card-header">
            <h2>服务状态</h2>
            <div class="card-status">运行正常</div>
          </div>
          <div class="card-content">
            <table class="service-table">
              <thead>
                <tr>
                  <th>#</th>
                  <th>服务名称</th>
                  <th>CPU</th>
                  <th>内存</th>
                  <th>磁盘</th>
                  <th>状态</th>
                </tr>
              </thead>
              <tbody>
                <tr v-for="(service, index) in serviceStatus" :key="index">
                  <td>{{ index + 1 }}</td>
                  <td>{{ service.name }}</td>
                  <td>{{ service.cpu }}%</td>
                  <td>{{ service.memory }}%</td>
                  <td>{{ service.disk }}%</td>
                  <td class="status-success">{{ service.status }}</td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
        
        <!-- 设备分布饼图 -->
        <div class="dashboard-card">
          <div class="card-header">
            <h2>设备分布</h2>
            <div class="card-status">实时数据</div>
          </div>
          <div class="card-content">
            <div ref="pieChartRef" class="chart-container"></div>
          </div>
        </div>
        
        <!-- 区域分布饼图 -->
        <div class="dashboard-card">
          <div class="card-header">
            <h2>区域分布</h2>
            <div class="card-status">实时数据</div>
          </div>
          <div class="card-content">
            <div ref="regionChartRef" class="chart-container"></div>
          </div>
        </div>
        
        <!-- 历史趋势线图 -->
        <div class="dashboard-card">
          <div class="card-header">
            <h2>数据趋势统计</h2>
            <div class="card-status">实时更新</div>
          </div>
          <div class="card-content">
            <div ref="lineChartRef" class="chart-container"></div>
          </div>
        </div>
        
        <!-- 交易量柱状图 -->
        <div class="dashboard-card">
          <div class="card-header">
            <h2>交易量数据统计</h2>
            <div class="card-status">实时更新</div>
          </div>
          <div class="card-content">
            <div ref="barChartRef" class="chart-container"></div>
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
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(2, auto);
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
  grid-column: span 3;
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

.chart-container {
  width: 100%;
  height: 300px;
  margin: 0 auto;
}

.service-table {
  width: 100%;
  border-collapse: collapse;
}

.service-table th {
  background-color: #002140;
  padding: 10px;
  text-align: left;
  color: #41b0d3;
  font-weight: normal;
}

.service-table td {
  padding: 8px 10px;
  border-bottom: 1px solid #003a6d;
}

.service-table tr:hover {
  background-color: #002140;
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
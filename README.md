# Realtime-Process-Monitoring-Dashboard
A real-time process monitoring dashboard provides a visual representation of key performance indicators (KPIs) and metrics, automatically updating with the latest data to offer immediate insights into the performance of a system, process, or business function.

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Real-Time Process Monitoring Dashboard</title>
    <style>
        :root {
            --primary-color: #3498db;
            --secondary-color: #2ecc71;
            --danger-color: #e74c3c;
            --warning-color: #f39c12;
            --dark-color: #2c3e50;
            --light-color: #ecf0f1;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #f5f7fa;
            color: #333;
        }
        
        .container {
            max-width: 1400px;
            margin: 0 auto;
            padding: 20px;
        }
        
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 30px;
            padding-bottom: 15px;
            border-bottom: 1px solid #ddd;
        }
        
        h1 {
            color: var(--dark-color);
        }
        
        .status-bar {
            display: flex;
            gap: 15px;
        }
        
        .status-item {
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .status-indicator {
            width: 12px;
            height: 12px;
            border-radius: 50%;
        }
        
        .online {
            background-color: var(--secondary-color);
        }
        
        .offline {
            background-color: var(--danger-color);
        }
        
        .dashboard {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-bottom: 20px;
        }
        
        .card {
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            padding: 20px;
        }
        
        .card-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 15px;
        }
        
        .card-title {
            font-size: 18px;
            font-weight: 600;
            color: var(--dark-color);
        }
        
        .chart-container {
            height: 250px;
            position: relative;
        }
        
        .chart-controls {
            display: flex;
            justify-content: flex-end;
            gap: 10px;
            margin-top: 10px;
        }
        
        .chart-btn {
            padding: 5px 10px;
            background-color: var(--light-color);
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 12px;
        }
        
        .chart-btn:hover {
            background-color: #ddd;
        }
        
        .process-list {
            grid-column: span 2;
        }
        
        table {
            width: 100%;
            border-collapse: collapse;
        }
        
        th, td {
            padding: 12px 15px;
            text-align: left;
            border-bottom: 1px solid #eee;
        }
        
        th {
            background-color: var(--light-color);
            font-weight: 600;
        }
        
        tr:hover {
            background-color: #f9f9f9;
        }
        
        .badge {
            padding: 4px 8px;
            border-radius: 4px;
            font-size: 12px;
            font-weight: 600;
        }
        
        .running {
            background-color: #d4edda;
            color: #155724;
        }
        
        .sleeping {
            background-color: #fff3cd;
            color: #856404;
        }
        
        .stopped {
            background-color: #f8d7da;
            color: #721c24;
        }
        
        .zombie {
            background-color: #d6d8d9;
            color: #1b1e21;
        }
        
        .action-btn {
            padding: 5px 10px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 12px;
            margin-right: 5px;
        }
        
        .kill-btn {
            background-color: var(--danger-color);
            color: white;
        }
        
        .restart-btn {
            background-color: var(--warning-color);
            color: white;
        }
        
        .priority-select {
            padding: 4px;
            border-radius: 4px;
            border: 1px solid #ddd;
        }
        
        .search-bar {
            margin-bottom: 20px;
            display: flex;
            gap: 10px;
        }
        
        .search-input {
            flex: 1;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        
        .filter-select {
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            background-color: white;
        }
        
        .time-range-selector {
            display: flex;
            justify-content: center;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        .time-range-btn {
            padding: 8px 15px;
            background-color: white;
            border: 1px solid #ddd;
            border-radius: 4px;
            cursor: pointer;
        }
        
        .time-range-btn.active {
            background-color: var(--primary-color);
            color: white;
            border-color: var(--primary-color);
        }
        
        .action-controls {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
            flex-wrap: wrap;
        }
        
        .action-group {
            display: flex;
            gap: 5px;
            align-items: center;
            background-color: var(--light-color);
            padding: 8px 12px;
            border-radius: 4px;
        }
        
        .action-label {
            font-size: 14px;
            font-weight: 600;
        }
        
        .bulk-actions {
            display: flex;
            gap: 10px;
            margin-top: 15px;
            padding-top: 15px;
            border-top: 1px solid #eee;
        }
        
        .bulk-btn {
            padding: 8px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-weight: 600;
        }
        
        .bulk-kill {
            background-color: var(--danger-color);
            color: white;
        }
        
        .bulk-restart {
            background-color: var(--warning-color);
            color: white;
        }
        
        .select-all {
            margin-right: 15px;
        }
        
        @media (max-width: 768px) {
            .dashboard {
                grid-template-columns: 1fr;
            }
            
            .process-list {
                grid-column: span 1;
            }
            
            .action-controls {
                flex-direction: column;
            }
            
            .action-group {
                width: 100%;
                justify-content: space-between;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>Process Monitoring Dashboard</h1>
            <div class="status-bar">
                <div class="status-item">
                    <div class="status-indicator online"></div>
                    <span>System Online</span>
                </div>
                <div class="status-item">
                    <span id="current-time">Loading time...</span>
                </div>
            </div>
        </header>
        
        <div class="time-range-selector">
            <button class="time-range-btn active" data-minutes="5">5 min</button>
            <button class="time-range-btn" data-minutes="15">15 min</button>
            <button class="time-range-btn" data-minutes="30">30 min</button>
            <button class="time-range-btn" data-minutes="60">1 hour</button>
        </div>
        
        <div class="search-bar">
            <input type="text" class="search-input" placeholder="Search processes..." id="processSearch">
            <select class="filter-select" id="statusFilter">
                <option value="all">All Statuses</option>
                <option value="running">Running</option>
                <option value="sleeping">Sleeping</option>
                <option value="stopped">Stopped</option>
                <option value="zombie">Zombie</option>
            </select>
        </div>
        
        <div class="action-controls">
            <div class="action-group">
                <span class="action-label">Filter Actions:</span>
                <select class="filter-select" id="actionFilter">
                    <option value="all">All Actions</option>
                    <option value="kill">Kill</option>
                    <option value="restart">Restart</option>
                    <option value="priority">Priority Change</option>
                </select>
            </div>
            <div class="action-group">
                <span class="action-label">CPU Threshold:</span>
                <input type="number" id="cpuThreshold" placeholder="CPU %" min="0" max="100" class="filter-select" style="width: 80px;">
            </div>
            <div class="action-group">
                <span class="action-label">Memory Threshold:</span>
                <input type="number" id="memoryThreshold" placeholder="Memory %" min="0" max="100" class="filter-select" style="width: 80px;">
            </div>
            <div class="action-group">
                <span class="action-label">PID Range:</span>
                <input type="number" id="pidMin" placeholder="Min PID" class="filter-select" style="width: 80px;">
                <span>-</span>
                <input type="number" id="pidMax" placeholder="Max PID" class="filter-select" style="width: 80px;">
            </div>
        </div>
        
        <div class="dashboard">
            <div class="card">
                <div class="card-header">
                    <div class="card-title">CPU Usage</div>
                    <div id="cpu-percentage">0%</div>
                </div>
                <div class="chart-container">
                    <canvas id="cpuChart"></canvas>
                </div>
                <div class="chart-controls">
                    <button class="chart-btn" id="resetCpuZoom">Reset Zoom</button>
                    <button class="chart-btn" id="exportCpuData">Export Data</button>
                </div>
            </div>
            
            <div class="card">
                <div class="card-header">
                    <div class="card-title">Memory Usage</div>
                    <div id="memory-percentage">0%</div>
                </div>
                <div class="chart-container">
                    <canvas id="memoryChart"></canvas>
                </div>
                <div class="chart-controls">
                    <button class="chart-btn" id="resetMemoryZoom">Reset Zoom</button>
                    <button class="chart-btn" id="exportMemoryData">Export Data</button>
                </div>
            </div>
            
            <div class="card process-list">
                <div class="card-header">
                    <div class="card-title">Running Processes</div>
                    <div id="process-count">0 processes</div>
                </div>
                <div class="bulk-actions">
                    <div class="select-all">
                        <input type="checkbox" id="selectAllProcesses">
                        <label for="selectAllProcesses">Select All</label>
                    </div>
                    <button class="bulk-btn bulk-kill" id="bulkKill">Kill Selected</button>
                    <button class="bulk-btn bulk-restart" id="bulkRestart">Restart Selected</button>
                </div>
                <div class="table-responsive">
                    <table id="processTable">
                        <thead>
                            <tr>
                                <th width="40px"></th>
                                <th>PID</th>
                                <th>Name</th>
                                <th>Status</th>
                                <th>CPU %</th>
                                <th>Memory %</th>
                                <th>Actions</th>
                            </tr>
                        </thead>
                        <tbody id="processTableBody">
                            <!-- Process rows will be inserted here -->
                        </tbody>
                    </table>
                </div>
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-zoom"></script>
    <script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-datalabels@2.0.0"></script>
    <script>
        // Initialize time labels
        function generateTimeLabels(minutes) {
            const labels = [];
            const now = new Date();
            
            for (let i = minutes; i >= 0; i--) {
                const time = new Date(now.getTime() - i * 60000);
                labels.push(time.toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'}));
            }
            
            return labels;
        }
        
        // Initialize charts with zoom plugin
        Chart.register(ChartZoom);
        
        const cpuCtx = document.getElementById('cpuChart').getContext('2d');
        const memoryCtx = document.getElementById('memoryChart').getContext('2d');
        
        let currentTimeRange = 5; // minutes
        let timeLabels = generateTimeLabels(currentTimeRange);
        
        const cpuChart = new Chart(cpuCtx, {
            type: 'line',
            data: {
                labels: timeLabels,
                datasets: [{
                    label: 'CPU Usage',
                    data: Array(timeLabels.length).fill(0),
                    borderColor: 'rgba(52, 152, 219, 1)',
                    backgroundColor: 'rgba(52, 152, 219, 0.1)',
                    borderWidth: 2,
                    tension: 0.4,
                    fill: true,
                    pointBackgroundColor: 'rgba(52, 152, 219, 1)',
                    pointHoverRadius: 6,
                    pointHitRadius: 10
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        display: false
                    },
                    tooltip: {
                        mode: 'index',
                        intersect: false,
                        callbacks: {
                            label: function(context) {
                                return `${context.dataset.label}: ${context.parsed.y.toFixed(1)}%`;
                            }
                        }
                    },
                    zoom: {
                        zoom: {
                            wheel: {
                                enabled: true,
                            },
                            pinch: {
                                enabled: true
                            },
                            mode: 'x',
                        },
                        pan: {
                            enabled: true,
                            mode: 'x',
                        },
                        limits: {
                            x: { min: 'original', max: 'original' },
                            y: { min: 0, max: 100 }
                        }
                    }
                },
                interaction: {
                    mode: 'nearest',
                    axis: 'x',
                    intersect: false
                },
                scales: {
                    y: {
                        beginAtZero: true,
                        max: 100,
                        ticks: {
                            callback: function(value) {
                                return value + '%';
                            }
                        }
                    },
                    x: {
                        grid: {
                            display: false
                        }
                    }
                }
            }
        });
        
        const memoryChart = new Chart(memoryCtx, {
            type: 'line',
            data: {
                labels: timeLabels,
                datasets: [{
                    label: 'Memory Usage',
                    data: Array(timeLabels.length).fill(0),
                    borderColor: 'rgba(46, 204, 113, 1)',
                    backgroundColor: 'rgba(46, 204, 113, 0.1)',
                    borderWidth: 2,
                    tension: 0.4,
                    fill: true,
                    pointBackgroundColor: 'rgba(46, 204, 113, 1)',
                    pointHoverRadius: 6,
                    pointHitRadius: 10
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: {
                        display: false
                    },
                    tooltip: {
                        mode: 'index',
                        intersect: false,
                        callbacks: {
                            label: function(context) {
                                return `${context.dataset.label}: ${context.parsed.y.toFixed(1)}%`;
                            }
                        }
                    },
                    zoom: {
                        zoom: {
                            wheel: {
                                enabled: true,
                            },
                            pinch: {
                                enabled: true
                            },
                            mode: 'x',
                        },
                        pan: {
                            enabled: true,
                            mode: 'x',
                        },
                        limits: {
                            x: { min: 'original', max: 'original' },
                            y: { min: 0, max: 100 }
                        }
                    }
                },
                interaction: {
                    mode: 'nearest',
                    axis: 'x',
                    intersect: false
                },
                scales: {
                    y: {
                        beginAtZero: true,
                        max: 100,
                        ticks: {
                            callback: function(value) {
                                return value + '%';
                            }
                        }
                    },
                    x: {
                        grid: {
                            display: false
                        }
                    }
                }
            }
        });
        
        // Update current time
        function updateCurrentTime() {
            const now = new Date();
            document.getElementById('current-time').textContent = now.toLocaleString();
        }
        
        setInterval(updateCurrentTime, 1000);
        updateCurrentTime();
        
        // Simulate real-time data updates
        function generateRandomProcesses() {
            const processNames = [
                'node', 'chrome', 'firefox', 'python', 'java', 
                'mysqld', 'nginx', 'docker', 'vscode', 'bash',
                'ssh', 'systemd', 'redis-server', 'postgres', 'php'
            ];
            
            const statuses = ['running', 'sleeping', 'stopped', 'zombie'];
            
            const processes = [];
            const processCount = Math.floor(Math.random() * 15) + 10; // 10-25 processes
            
            for (let i = 0; i < processCount; i++) {
                const pid = Math.floor(Math.random() * 9000) + 1000;
                const name = processNames[Math.floor(Math.random() * processNames.length)];
                const status = statuses[Math.floor(Math.random() * statuses.length)];
                const cpu = Math.random() * 30;
                const memory = Math.random() * 20;
                
                processes.push({
                    pid,
                    name,
                    status,
                    cpu: parseFloat(cpu.toFixed(1)),
                    memory: parseFloat(memory.toFixed(1))
                });
            }
            
            // Sort by CPU usage (descending)
            return processes.sort((a, b) => b.cpu - a.cpu);
        }
        
        function updateProcessTable(processes) {
            const tableBody = document.getElementById('processTableBody');
            tableBody.innerHTML = '';
            
            processes.forEach(process => {
                const row = document.createElement('tr');
                const rowId = `process-${process.pid}`;
                row.id = rowId;
                
                // Determine status badge class
                let statusClass = '';
                switch(process.status) {
                    case 'running': statusClass = 'running'; break;
                    case 'sleeping': statusClass = 'sleeping'; break;
                    case 'stopped': statusClass = 'stopped'; break;
                    case 'zombie': statusClass = 'zombie'; break;
                }
                
                row.innerHTML = `
                    <td><input type="checkbox" class="process-checkbox" data-pid="${process.pid}"></td>
                    <td>${process.pid}</td>
                    <td>${process.name}</td>
                    <td><span class="badge ${statusClass}">${process.status}</span></td>
                    <td>${process.cpu}%</td>
                    <td>${process.memory}%</td>
                    <td>
                        <button class="action-btn kill-btn" data-pid="${process.pid}">Kill</button>
                        <button class="action-btn restart-btn" data-pid="${process.pid}">Restart</button>
                        <select class="priority-select" data-pid="${process.pid}">
                            <option>Priority</option>
                            <option value="high">High</option>
                            <option value="normal">Normal</option>
                            <option value="low">Low</option>
                        </select>
                    </td>
                `;
                
                tableBody.appendChild(row);
            });
            
            document.getElementById('process-count').textContent = `${processes.length} processes`;
            
            // Add event listeners to action buttons
            document.querySelectorAll('.kill-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const pid = this.getAttribute('data-pid');
                    const processName = this.closest('tr').querySelector('td:nth-child(3)').textContent;
                    if (confirm(`Are you sure you want to kill process ${pid} (${processName})?`)) {
                        // In a real app, you would send a request to the server to kill the process
                        document.getElementById(`process-${pid}`).style.opacity = '0.5';
                        document.getElementById(`process-${pid}`).querySelector('.kill-btn').disabled = true;
                        // Simulate process termination
                        setTimeout(() => {
                            document.getElementById(`process-${pid}`).remove();
                            updateProcessCount();
                        }, 500);
                    }
                });
            });
            
            document.querySelectorAll('.restart-btn').forEach(btn => {
                btn.addEventListener('click', function() {
                    const pid = this.getAttribute('data-pid');
                    const processName = this.closest('tr').querySelector('td:nth-child(3)').textContent;
                    if (confirm(`Are you sure you want to restart process ${pid} (${processName})?`)) {
                        // In a real app, you would send a request to the server to restart the process
                        const row = document.getElementById(`process-${pid}`);
                        row.style.backgroundColor = 'rgba(255, 193, 7, 0.2)';
                        setTimeout(() => {
                            row.style.backgroundColor = '';
                        }, 1000);
                    }
                });
            });
            
            document.querySelectorAll('.priority-select').forEach(select => {
                select.addEventListener('change', function() {
                    const pid = this.getAttribute('data-pid');
                    const priority = this.value;
                    if (priority !== 'Priority') {
                        // In a real app, you would send a request to the server to change priority
                        const row = document.getElementById(`process-${pid}`);
                        const statusCell = row.querySelector('td:nth-child(4)');
                        statusCell.innerHTML = `<span class="badge running">priority:${priority}</span>`;
                    }
                });
            });
            
            // Add event listeners to checkboxes
            document.querySelectorAll('.process-checkbox').forEach(checkbox => {
                checkbox.addEventListener('change', function() {
                    updateSelectAllCheckbox();
                });
            });
            
            updateSelectAllCheckbox();
            filterProcesses();
        }
        
        function updateProcessCount() {
            const visibleRows = document.querySelectorAll('#processTableBody tr:not([style*="display: none"])');
            document.getElementById('process-count').textContent = `${visibleRows.length} processes`;
        }
        
        function updateSelectAllCheckbox() {
            const checkboxes = document.querySelectorAll('.process-checkbox:not([style*="display: none"])');
            const checkedCheckboxes = document.querySelectorAll('.process-checkbox:not([style*="display: none"]):checked');
            const selectAll = document.getElementById('selectAllProcesses');
            
            if (checkboxes.length === checkedCheckboxes.length && checkboxes.length > 0) {
                selectAll.checked = true;
                selectAll.indeterminate = false;
            } else if (checkedCheckboxes.length > 0) {
                selectAll.checked = false;
                selectAll.indeterminate = true;
            } else {
                selectAll.checked = false;
                selectAll.indeterminate = false;
            }
        }
        
        function updateCharts(cpuUsage, memoryUsage) {
            // Shift data and add new point
            const now = new Date();
            const currentTime = now.toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});
            
            // Update CPU chart
            cpuChart.data.labels.shift();
            cpuChart.data.labels.push(currentTime);
            cpuChart.data.datasets[0].data.shift();
            cpuChart.data.datasets[0].data.push(cpuUsage);
            cpuChart.update();
            
            // Update Memory chart
            memoryChart.data.labels.shift();
            memoryChart.data.labels.push(currentTime);
            memoryChart.data.datasets[0].data.shift();
            memoryChart.data.datasets[0].data.push(memoryUsage);
            memoryChart.update();
            
            // Update percentage displays
            document.getElementById('cpu-percentage').textContent = `${cpuUsage.toFixed(1)}%`;
            document.getElementById('memory-percentage').textContent = `${memoryUsage.toFixed(1)}%`;
        }
        
        function simulateSystemMetrics() {
            // Generate random CPU and memory usage (between 10% and 90%)
            const cpuUsage = 10 + Math.random() * 80;
            const memoryUsage = 10 + Math.random() * 80;
            
            updateCharts(cpuUsage, memoryUsage);
            
            // Generate random processes
            const processes = generateRandomProcesses();
            updateProcessTable(processes);
        }
        
        // Initial data load
        simulateSystemMetrics();
        
        // Update data every 3 seconds
        const dataInterval = setInterval(simulateSystemMetrics, 3000);
        
        // Search and filter functionality
        document.getElementById('processSearch').addEventListener('input', function() {
            filterProcesses();
        });
        
        document.getElementById('statusFilter').addEventListener('change', function() {
            filterProcesses();
        });
        
        document.getElementById('actionFilter').addEventListener('change', function() {
            filterProcesses();
        });
        
        document.getElementById('cpuThreshold').addEventListener('input', function() {
            filterProcesses();
        });
        
        document.getElementById('memoryThreshold').addEventListener('input', function() {
            filterProcesses();
        });
        
        document.getElementById('pidMin').addEventListener('input', function() {
            filterProcesses();
        });
        
        document.getElementById('pidMax').addEventListener('input', function() {
            filterProcesses();
        });
        
        function filterProcesses() {
            const searchTerm = document.getElementById('processSearch').value.toLowerCase();
            const statusFilter = document.getElementById('statusFilter').value;
            const actionFilter = document.getElementById('actionFilter').value;
            const cpuThreshold = parseFloat(document.getElementById('cpuThreshold').value) || 0;
            const memoryThreshold = parseFloat(document.getElementById('memoryThreshold').value) || 0;
            const pidMin = parseInt(document.getElementById('pidMin').value) || 0;
            const pidMax = parseInt(document.getElementById('pidMax').value) || Infinity;
            
            const rows = document.querySelectorAll('#processTableBody tr');
            
            rows.forEach(row => {
                const pid = parseInt(row.cells[1].textContent);
                const name = row.cells[2].textContent.toLowerCase();
                const status = row.cells[3].textContent.toLowerCase();
                const cpu = parseFloat(row.cells[4].textContent);
                const memory = parseFloat(row.cells[5].textContent);
                const hasKillBtn = row.querySelector('.kill-btn') !== null;
                const hasRestartBtn = row.querySelector('.restart-btn') !== null;
                const hasPrioritySelect = row.querySelector('.priority-select') !== null;
                
                // Apply all filters
                const nameMatch = name.includes(searchTerm);
                const statusMatch = statusFilter === 'all' || status.includes(statusFilter);
                const cpuMatch = cpu >= cpuThreshold;
                const memoryMatch = memory >= memoryThreshold;
                const pidMatch = pid >= pidMin && pid <= pidMax;
                
                // Action filter logic
                let actionMatch = true;
                if (actionFilter !== 'all') {
                    if (actionFilter === 'kill') {
                        actionMatch = hasKillBtn;
                    } else if (actionFilter === 'restart') {
                        actionMatch = hasRestartBtn;
                    } else if (actionFilter === 'priority') {
                        actionMatch = hasPrioritySelect;
                    }
                }
                
                if (nameMatch && statusMatch && cpuMatch && memoryMatch && pidMatch && actionMatch) {
                    row.style.display = '';
                } else {
                    row.style.display = 'none';
                }
            });
            
            updateProcessCount();
            updateSelectAllCheckbox();
        }
        
        // Chart controls
        document.getElementById('resetCpuZoom').addEventListener('click', function() {
            cpuChart.resetZoom();
        });
        
        document.getElementById('resetMemoryZoom').addEventListener('click', function() {
            memoryChart.resetZoom();
        });
        
        document.getElementById('exportCpuData').addEventListener('click', function() {
            exportChartData(cpuChart, 'CPU Usage Data');
        });
        
        document.getElementById('exportMemoryData').addEventListener('click', function() {
            exportChartData(memoryChart, 'Memory Usage Data');
        });
        
        function exportChartData(chart, filename) {
            let csvContent = "Time,Value\n";
            
            for (let i = 0; i < chart.data.labels.length; i++) {
                csvContent += `${chart.data.labels[i]},${chart.data.datasets[0].data[i]}\n`;
            }
            
            const blob = new Blob([csvContent], { type: 'text/csv;charset=utf-8;' });
            const url = URL.createObjectURL(blob);
            const link = document.createElement('a');
            link.setAttribute('href', url);
            link.setAttribute('download', `${filename}.csv`);
            link.style.visibility = 'hidden';
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        }
        
        // Time range selector
        document.querySelectorAll('.time-range-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                // Update active button
                document.querySelectorAll('.time-range-btn').forEach(b => b.classList.remove('active'));
                this.classList.add('active');
                
                // Get new time range
                currentTimeRange = parseInt(this.getAttribute('data-minutes'));
                
                // Clear interval and restart with new data frequency
                clearInterval(dataInterval);
                
                // Generate new labels
                timeLabels = generateTimeLabels(currentTimeRange);
                
                // Reset charts with new time range
                cpuChart.data.labels = [...timeLabels];
                cpuChart.data.datasets[0].data = Array(timeLabels.length).fill(0);
                cpuChart.update();
                
                memoryChart.data.labels = [...timeLabels];
                memoryChart.data.datasets[0].data = Array(timeLabels.length).fill(0);
                memoryChart.update();
                
                // Restart data simulation with new interval
                setInterval(simulateSystemMetrics, (currentTimeRange * 60000) / timeLabels.length);
            });
        });
        
        // Bulk actions
        document.getElementById('selectAllProcesses').addEventListener('change', function() {
            const checkboxes = document.querySelectorAll('.process-checkbox:not([style*="display: none"])');
            checkboxes.forEach(checkbox => {
                checkbox.checked = this.checked;
            });
        });
        
        document.getElementById('bulkKill').addEventListener('click', function() {
            const selectedPids = getSelectedProcesses();
            if (selectedPids.length === 0) {
                alert('Please select at least one process to kill');
                return;
            }
            
            if (confirm(`Are you sure you want to kill ${selectedPids.length} selected processes?`)) {
                // In a real app, you would send a request to the server to kill these processes
                selectedPids.forEach(pid => {
                    const row = document.getElementById(`process-${pid}`);
                    if (row) {
                        row.style.opacity = '0.5';
                        row.querySelector('.kill-btn').disabled = true;
                        // Simulate process termination
                        setTimeout(() => {
                            row.remove();
                            updateProcessCount();
                        }, 500);
                    }
                });
            }
        });
        
        document.getElementById('bulkRestart').addEventListener('click', function() {
            const selectedPids = getSelectedProcesses();
            if (selectedPids.length === 0) {
                alert('Please select at least one process to restart');
                return;
            }
            
            if (confirm(`Are you sure you want to restart ${selectedPids.length} selected processes?`)) {
                // In a real app, you would send a request to the server to restart these processes
                selectedPids.forEach(pid => {
                    const row = document.getElementById(`process-${pid}`);
                    if (row) {
                        row.style.backgroundColor = 'rgba(255, 193, 7, 0.2)';
                        setTimeout(() => {
                            row.style.backgroundColor = '';
                        }, 1000);
                    }
                });
            }
        });
        
        function getSelectedProcesses() {
            const checkboxes = document.querySelectorAll('.process-checkbox:checked:not([style*="display: none"])');
            return Array.from(checkboxes).map(checkbox => parseInt(checkbox.getAttribute('data-pid')));
        }
    </script>
</body>
</html>

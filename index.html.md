#   
<!DOCTYPE html>  
<html lang="zh-CN">  
<head>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
    <title>随机抽查学生姓名系统</title>  
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">  
    <style>  
        * {  
            margin: 0;  
            padding: 0;  
            box-sizing: border-box;  
            font-family: 'Segoe UI', 'Microsoft YaHei', sans-serif;  
        }  
          
        body {  
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);  
            color: #333;  
            min-height: 100vh;  
            padding: 20px;  
            display: flex;  
            flex-direction: column;  
            align-items: center;  
            justify-content: center;  
        }  
          
        .container {  
            max-width: 1200px;  
            width: 100%;  
            background-color: rgba(255, 255, 255, 0.95);  
            border-radius: 20px;  
            box-shadow: 0 15px 35px rgba(0, 0, 0, 0.2);  
            padding: 30px;  
            margin: 20px;  
            overflow: hidden;  
        }  
          
        header {  
            text-align: center;  
            margin-bottom: 30px;  
        }  
          
        .main-title {  
            font-size: 3.5rem;  
            color: #2575fc;  
            text-shadow: 3px 3px 0 rgba(37, 117, 252, 0.1);  
            margin-bottom: 10px;  
            position: relative;  
            display: inline-block;  
            padding: 0 15px;  
        }  
          
        .main-title::after {  
            content: "";  
            position: absolute;  
            bottom: -10px;  
            left: 15%;  
            width: 70%;  
            height: 5px;  
            background: linear-gradient(to right, transparent, #ff0080, transparent);  
            border-radius: 5px;  
        }  
          
        .subtitle {  
            font-size: 1.3rem;  
            color: #666;  
            margin-top: 10px;  
        }  
          
        .content-wrapper {  
            display: flex;  
            flex-wrap: wrap;  
            gap: 30px;  
        }  
          
        .left-panel {  
            flex: 1;  
            min-width: 300px;  
        }  
          
        .right-panel {  
            flex: 1;  
            min-width: 300px;  
        }  
          
        .panel {  
            background: white;  
            border-radius: 15px;  
            padding: 25px;  
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.08);  
            margin-bottom: 25px;  
            border: 1px solid #eaeaea;  
        }  
          
        .panel-title {  
            font-size: 1.8rem;  
            color: #2575fc;  
            margin-bottom: 20px;  
            padding-bottom: 10px;  
            border-bottom: 2px dashed #eaeaea;  
            display: flex;  
            align-items: center;  
            gap: 10px;  
        }  
          
        .panel-title i {  
            color: #ff0080;  
        }  
          
        .name-display {  
            text-align: center;  
            padding: 30px;  
            background: linear-gradient(135deg, #f5f7fa 0%, #e4edf5 100%);  
            border-radius: 15px;  
            margin-bottom: 25px;  
            border: 3px dashed #c3d7f3;  
            min-height: 200px;  
            display: flex;  
            flex-direction: column;  
            justify-content: center;  
            align-items: center;  
            transition: all 0.3s ease;  
        }  
          
        .selected-name {  
            font-size: 3.5rem;  
            font-weight: 800;  
            color: #2575fc;  
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);  
            margin: 10px 0;  
            min-height: 90px;  
            display: flex;  
            align-items: center;  
            justify-content: center;  
            transition: all 0.2s;  
        }  
          
        .name-placeholder {  
            font-size: 1.5rem;  
            color: #aaa;  
            font-weight: normal;  
        }  
          
        .button-container {  
            display: flex;  
            flex-wrap: wrap;  
            gap: 15px;  
            justify-content: center;  
            margin-top: 20px;  
        }  
          
        .btn {  
            padding: 15px 30px;  
            border: none;  
            border-radius: 50px;  
            font-size: 1.2rem;  
            font-weight: 600;  
            cursor: pointer;  
            transition: all 0.3s ease;  
            display: flex;  
            align-items: center;  
            justify-content: center;  
            gap: 10px;  
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);  
        }  
          
        .btn-primary {  
            background: linear-gradient(to right, #2575fc, #6a11cb);  
            color: white;  
            flex: 1;  
            min-width: 200px;  
        }  
          
        .btn-primary:hover {  
            transform: translateY(-5px);  
            box-shadow: 0 10px 20px rgba(37, 117, 252, 0.3);  
        }  
          
        .btn-secondary {  
            background: linear-gradient(to right, #ff7e5f, #feb47b);  
            color: white;  
            flex: 1;  
            min-width: 200px;  
        }  
          
        .btn-secondary:hover {  
            transform: translateY(-5px);  
            box-shadow: 0 10px 20px rgba(255, 126, 95, 0.3);  
        }  
          
        .btn:active {  
            transform: translateY(0);  
        }  
          
        .students-list {  
            display: grid;  
            grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));  
            gap: 12px;  
            max-height: 400px;  
            overflow-y: auto;  
            padding: 10px;  
        }  
          
        .student-item {  
            background: #f8f9ff;  
            border-radius: 10px;  
            padding: 12px 8px;  
            text-align: center;  
            font-weight: 500;  
            transition: all 0.2s;  
            border: 1px solid #e0e7ff;  
            cursor: default;  
        }  
          
        .student-item:hover {  
            transform: translateY(-3px);  
            background: #eef2ff;  
            box-shadow: 0 5px 10px rgba(37, 117, 252, 0.1);  
        }  
          
        .student-item.selected {  
            background: linear-gradient(135deg, #2575fc, #6a11cb);  
            color: white;  
            border-color: #2575fc;  
            font-weight: 600;  
            transform: scale(1.05);  
        }  
          
        .history-list {  
            max-height: 300px;  
            overflow-y: auto;  
            padding: 10px;  
        }  
          
        .history-item {  
            display: flex;  
            justify-content: space-between;  
            align-items: center;  
            padding: 15px;  
            background: #f8f9ff;  
            border-radius: 10px;  
            margin-bottom: 10px;  
            border-left: 5px solid #2575fc;  
        }  
          
        .history-name {  
            font-weight: 600;  
            font-size: 1.2rem;  
        }  
          
        .history-time {  
            color: #666;  
            font-size: 0.9rem;  
        }  
          
        .counter {  
            font-size: 1.2rem;  
            color: #666;  
            text-align: center;  
            margin-top: 15px;  
        }  
          
        .highlight {  
            color: #ff0080;  
            font-weight: 700;  
        }  
          
        .footer {  
            text-align: center;  
            margin-top: 30px;  
            color: rgba(255, 255, 255, 0.8);  
            font-size: 0.9rem;  
            padding: 20px;  
        }  
          
        /* 动画效果 */  
        @keyframes pulse {  
            0% { transform: scale(1); }  
            50% { transform: scale(1.05); }  
            100% { transform: scale(1); }  
        }  
          
        .pulse {  
            animation: pulse 0.5s ease-in-out;  
        }  
          
        @keyframes highlight {  
            0% { background-color: #fff; }  
            50% { background-color: #f0f8ff; }  
            100% { background-color: #fff; }  
        }  
          
        .highlight-animation {  
            animation: highlight 1s ease;  
        }  
          
        /* 响应式设计 */  
        @media (max-width: 768px) {  
            .content-wrapper {  
                flex-direction: column;  
            }  
              
            .main-title {  
                font-size: 2.5rem;  
            }  
              
            .selected-name {  
                font-size: 2.5rem;  
            }  
              
            .btn {  
                padding: 12px 20px;  
                font-size: 1.1rem;  
            }  
              
            .students-list {  
                grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));  
            }  
        }  
          
        @media (max-width: 480px) {  
            .container {  
                padding: 20px 15px;  
            }  
              
            .main-title {  
                font-size: 2rem;  
            }  
              
            .panel-title {  
                font-size: 1.5rem;  
            }  
              
            .selected-name {  
                font-size: 2rem;  
            }  
              
            .students-list {  
                grid-template-columns: repeat(auto-fill, minmax(80px, 1fr));  
            }  
        }  
    </style>  
</head>  
<body>  
    <div class="container">  
        <header>  
            <h1 class="main-title">就是你了</h1>  
            <p class="subtitle">随机抽查学生姓名系统 - 公平公正的随机点名工具</p>  
        </header>  
          
        <div class="content-wrapper">  
            <div class="left-panel">  
                <div class="panel name-display">  
                    <h2 class="panel-title"><i class="fas fa-user-check"></i> 当前选中</h2>  
                    <div class="selected-name">  
                        <span class="name-placeholder">点击按钮开始随机抽取</span>  
                    </div>  
                    <div class="counter">  
                        已抽取: <span class="highlight" id="selected-count">0</span> 次  
                    </div>  
                </div>  
                  
                <div class="panel">  
                    <h2 class="panel-title"><i class="fas fa-random"></i> 抽取控制</h2>  
                    <div class="button-container">  
                        <button class="btn btn-primary" id="random-btn">  
                            <i class="fas fa-random"></i> 随机抽取一名学生  
                        </button>  
                        <button class="btn btn-secondary" id="reset-btn">  
                            <i class="fas fa-redo"></i> 重置抽取记录  
                        </button>  
                    </div>  
                    <div class="counter" style="margin-top: 20px;">  
                        剩余学生: <span class="highlight" id="remaining-count">69</span> 名  
                    </div>  
                </div>  
                  
                <div class="panel">  
                    <h2 class="panel-title"><i class="fas fa-history"></i> 抽取历史</h2>  
                    <div class="history-list" id="history-list">  
                        <!-- 历史记录将通过JavaScript动态添加 -->  
                        <div class="history-empty">暂无抽取记录</div>  
                    </div>  
                </div>  
            </div>  
              
            <div class="right-panel">  
                <div class="panel">  
                    <h2 class="panel-title"><i class="fas fa-list-ol"></i> 学生名单 (共69人)</h2>  
                    <div class="students-list" id="students-list">  
                        <!-- 学生名单将通过JavaScript动态添加 -->  
                    </div>  
                </div>  
                  
                <div class="panel">  
                    <h2 class="panel-title"><i class="fas fa-info-circle"></i> 使用说明</h2>  
                    <ul style="padding-left: 20px; line-height: 1.8; color: #555;">  
                        <li>点击"随机抽取一名学生"按钮开始随机点名</li>  
                        <li>系统会高亮显示被选中的学生</li>  
                        <li>抽取记录会保存在右侧"抽取历史"中</li>  
                        <li>已被选中的学生不会在后续抽取中被重复选中</li>  
                        <li>点击"重置抽取记录"可以重新开始抽取</li>  
                        <li>点击学生名单中的名字可以手动选中该学生</li>  
                    </ul>  
                </div>  
            </div>  
        </div>  
    </div>  
      
    <div class="footer">  
        <p>随机抽查学生姓名系统 &copy; 2023 | 学生总数: 69人 | 设计: 前端开发</p>  
    </div>  
  
    <script>  
        // 学生名单数据  
        const students = [  
            "彭静茹", "刘宇彤", "陈芝攸", "赵娜", "邓思佳",   
            "洪扬扬", "杨婷", "赖逸凡", "于夕圆", "王雨洁",   
            "李海缘", "和元英", "吴溶溶", "王一航", "陈志东",   
            "赵云江", "强东俊", "尹泽", "毛顺凯", "杜凤江",   
            "尹才源", "王丁", "郑在", "栗晨航", "池泽磊",   
            "石泽阳", "何林茂", "徐世龙", "梁文林", "郑恩宇",   
            "张子童", "张禾鹏", "江嘉荣", "李光恒", "赵建强",   
            "邹毅", "孙琬婷", "宋美盈", "李叶青", "潘和平",   
            "王恩琪", "胡玥帆", "陈定莉", "马婕庭", "马雨凤",   
            "张潇晗", "焦佳慧", "陈启宇", "叶红毅", "王紫如",   
            "刘景丹", "王梦", "张瑞雪", "施韩苗", "王国苹",   
            "冯应紫", "张子琪", "郑贤杰", "张云翔", "周子尧",   
            "钟凡", "朱子豪", "张云博", "樊佳玮", "任武赫",   
            "田东鑫", "张子煜", "许国栋", "于展翔", "王嘉旭",   
            "赵思静", "邵新意", "李继婧"  
        ];  
          
        // 初始化变量  
        let remainingStudents = [...students];  
        let selectedStudents = [];  
        let selectedCount = 0;  
        let isSelecting = false;  
          
        // DOM元素  
        const studentsListEl = document.getElementById('students-list');  
        const selectedNameEl = document.querySelector('.selected-name');  
        const historyListEl = document.getElementById('history-list');  
        const randomBtn = document.getElementById('random-btn');  
        const resetBtn = document.getElementById('reset-btn');  
        const selectedCountEl = document.getElementById('selected-count');  
        const remainingCountEl = document.getElementById('remaining-count');  
          
        // 初始化学生名单  
        function initStudentsList() {  
            studentsListEl.innerHTML = '';  
            students.forEach(student => {  
                const studentItem = document.createElement('div');  
                studentItem.className = 'student-item';  
                studentItem.textContent = student;  
                studentItem.dataset.name = student;  
                  
                // 点击学生名字可以手动选中  
                studentItem.addEventListener('click', () => {  
                    if (!selectedStudents.includes(student)) {  
                        selectStudent(student);  
                    }  
                });  
                  
                studentsListEl.appendChild(studentItem);  
            });  
              
            updateCounters();  
        }  
          
        // 随机选择一名学生  
        function selectRandomStudent() {  
            if (isSelecting || remainingStudents.length === 0) return;  
              
            isSelecting = true;  
            randomBtn.disabled = true;  
              
            // 动画效果：快速切换名字  
            let iterations = 0;  
            const maxIterations = 20;  
            const interval = setInterval(() => {  
                // 随机显示一个名字（包括已选中的）  
                const randomIndex = Math.floor(Math.random() * students.length);  
                selectedNameEl.textContent = students[randomIndex];  
                selectedNameEl.classList.add('pulse');  
                  
                iterations++;  
                  
                if (iterations >= maxIterations) {  
                    clearInterval(interval);  
                      
                    // 最终选择  
                    const finalIndex = Math.floor(Math.random() * remainingStudents.length);  
                    const selectedStudent = remainingStudents[finalIndex];  
                      
                    // 从剩余学生中移除  
                    remainingStudents.splice(finalIndex, 1);  
                      
                    // 添加到已选列表  
                    selectedStudents.push(selectedStudent);  
                      
                    // 更新显示  
                    setTimeout(() => {  
                        selectStudent(selectedStudent);  
                        isSelecting = false;  
                        randomBtn.disabled = false;  
                    }, 300);  
                }  
                  
                // 移除动画类，以便下次添加  
                setTimeout(() => {  
                    selectedNameEl.classList.remove('pulse');  
                }, 250);  
                  
            }, 100);  
        }  
          
        // 选择指定学生  
        function selectStudent(student) {  
            // 更新显示的名字  
            selectedNameEl.textContent = student;  
            selectedNameEl.classList.add('pulse');  
              
            // 高亮显示选中的学生  
            document.querySelectorAll('.student-item').forEach(item => {  
                item.classList.remove('selected');  
                if (item.dataset.name === student) {  
                    item.classList.add('selected');  
                    item.scrollIntoView({ behavior: 'smooth', block: 'center' });  
                }  
            });  
              
            // 添加到历史记录  
            addToHistory(student);  
              
            // 更新计数器  
            updateCounters();  
              
            // 添加整体高亮动画  
            document.querySelector('.name-display').classList.add('highlight-animation');  
            setTimeout(() => {  
                document.querySelector('.name-display').classList.remove('highlight-animation');  
            }, 1000);  
              
            // 移除动画类  
            setTimeout(() => {  
                selectedNameEl.classList.remove('pulse');  
            }, 500);  
        }  
          
        // 添加到历史记录  
        function addToHistory(student) {  
            // 移除"暂无抽取记录"提示  
            const emptyMsg = historyListEl.querySelector('.history-empty');  
            if (emptyMsg) emptyMsg.remove();  
              
            const historyItem = document.createElement('div');  
            historyItem.className = 'history-item';  
              
            const now = new Date();  
            const timeString = `${now.getHours().toString().padStart(2, '0')}:${now.getMinutes().toString().padStart(2, '0')}:${now.getSeconds().toString().padStart(2, '0')}`;  
              
            historyItem.innerHTML = `  
                <div class="history-name">${student}</div>  
                <div class="history-time">${timeString}</div>  
            `;  
              
            // 将新记录添加到最前面  
            historyListEl.insertBefore(historyItem, historyListEl.firstChild);  
              
            // 限制历史记录数量  
            if (historyListEl.children.length > 10) {  
                historyListEl.removeChild(historyListEl.lastChild);  
            }  
        }  
          
        // 更新计数器  
        function updateCounters() {  
            selectedCount = selectedStudents.length;  
            const remainingCount = remainingStudents.length;  
              
            selectedCountEl.textContent = selectedCount;  
            remainingCountEl.textContent = remainingCount;  
              
            // 更新按钮状态  
            randomBtn.disabled = remainingCount === 0;  
            if (remainingCount === 0) {  
                randomBtn.innerHTML = '<i class="fas fa-check"></i> 所有学生已抽取完毕';  
            } else {  
                randomBtn.innerHTML = '<i class="fas fa-random"></i> 随机抽取一名学生';  
            }  
        }  
          
        // 重置抽取记录  
        function resetSelection() {  
            if (selectedStudents.length === 0) return;  
              
            if (confirm("确定要重置所有抽取记录吗？这将清除所有已选中的学生。")) {  
                remainingStudents = [...students];  
                selectedStudents = [];  
                selectedNameEl.innerHTML = '<span class="name-placeholder">点击按钮开始随机抽取</span>';  
                  
                // 清除学生列表的高亮  
                document.querySelectorAll('.student-item').forEach(item => {  
                    item.classList.remove('selected');  
                });  
                  
                // 清除历史记录  
                historyListEl.innerHTML = '<div class="history-empty">暂无抽取记录</div>';  
                  
                // 更新计数器  
                updateCounters();  
                  
                // 显示重置成功提示  
                alert("抽取记录已重置，可以重新开始抽取。");  
            }  
        }  
          
        // 初始化  
        function init() {  
            initStudentsList();  
              
            // 绑定按钮事件  
            randomBtn.addEventListener('click', selectRandomStudent);  
            resetBtn.addEventListener('click', resetSelection);  
              
            // 添加键盘快捷键支持  
            document.addEventListener('keydown', (e) => {  
                // 空格键开始/停止随机抽取  
                if (e.code === 'Space' && !isSelecting && remainingStudents.length > 0) {  
                    e.preventDefault();  
                    selectRandomStudent();  
                }  
                  
                // R键重置  
                if (e.code === 'KeyR' && (e.ctrlKey || e.metaKey)) {  
                    e.preventDefault();  
                    resetSelection();  
                }  
            });  
              
            // 显示学生总数  
            console.log(`学生总数: ${students.length}人`);  
        }  
          
        // 页面加载完成后初始化  
        window.addEventListener('DOMContentLoaded', init);  
    </script>  
</body>  
</html>  

# hehe
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>人體賓果遊戲 - 填寫名字版</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Microsoft JhengHei', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .container {
            max-width: 1100px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            padding: 30px;
            margin-bottom: 20px;
        }

        h1 {
            text-align: center;
            color: #764ba2;
            margin-bottom: 20px;
            font-size: 2.5em;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
        }

        .controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            margin-bottom: 30px;
            flex-wrap: wrap;
        }

        button {
            padding: 12px 24px;
            font-size: 16px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .version-btn {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
        }

        .version-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(118, 75, 162, 0.4);
        }

        .version-btn.active {
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
        }

        .reset-btn {
            background: linear-gradient(135deg, #fa709a 0%, #fee140 100%);
            color: #333;
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(250, 112, 154, 0.4);
        }

        .export-btn {
            background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%);
            color: white;
        }

        .export-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(79, 172, 254, 0.4);
        }

        .bingo-grid {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 12px;
            margin-bottom: 20px;
        }

        .bingo-cell {
            border: 2px solid #667eea;
            border-radius: 10px;
            padding: 12px;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            transition: all 0.3s ease;
            position: relative;
            min-height: 140px;
            display: flex;
            flex-direction: column;
        }

        .bingo-cell:hover {
            transform: scale(1.02);
            box-shadow: 0 5px 15px rgba(102, 126, 234, 0.3);
        }

        .bingo-cell.completed {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }

        .bingo-cell.completed .cell-title {
            color: white;
        }

        .cell-title {
            font-size: 13px;
            font-weight: 600;
            color: #333;
            margin-bottom: 8px;
            line-height: 1.3;
            text-align: center;
            min-height: 36px;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .name-inputs {
            display: flex;
            flex-direction: column;
            gap: 5px;
            flex-grow: 1;
        }

        .name-input {
            width: 100%;
            padding: 6px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 12px;
            transition: all 0.2s ease;
        }

        .name-input:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 5px rgba(102, 126, 234, 0.3);
        }

        .name-input.filled {
            background-color: #e8f5e9;
            border-color: #4caf50;
        }

        .completed .name-input {
            background-color: rgba(255, 255, 255, 0.9);
            border-color: #fff;
        }

        .win-message {
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
            color: white;
            padding: 40px;
            border-radius: 20px;
            font-size: 2em;
            font-weight: bold;
            text-align: center;
            box-shadow: 0 20px 60px rgba(0,0,0,0.5);
            display: none;
            z-index: 1000;
            animation: winPop 0.5s ease;
        }

        @keyframes winPop {
            0% {
                transform: translate(-50%, -50%) scale(0);
            }
            50% {
                transform: translate(-50%, -50%) scale(1.2);
            }
            100% {
                transform: translate(-50%, -50%) scale(1);
            }
        }

        .win-message.show {
            display: block;
        }

        .stats {
            display: flex;
            justify-content: space-around;
            padding: 20px;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            border-radius: 10px;
            margin-bottom: 20px;
        }

        .stat-item {
            text-align: center;
        }

        .stat-label {
            font-size: 14px;
            color: #666;
            margin-bottom: 5px;
        }

        .stat-value {
            font-size: 24px;
            font-weight: bold;
            color: #764ba2;
        }

        .name-list {
            margin-top: 20px;
            padding: 20px;
            background: linear-gradient(135deg, #ffecd2 0%, #fcb69f 100%);
            border-radius: 10px;
            max-height: 300px;
            overflow-y: auto;
        }

        .name-list h3 {
            color: #764ba2;
            margin-bottom: 15px;
            font-size: 1.3em;
        }

        .name-entry {
            padding: 8px;
            margin-bottom: 8px;
            background: white;
            border-radius: 8px;
            font-size: 14px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .name-entry strong {
            color: #764ba2;
            margin-right: 10px;
        }

        .clear-cell-btn {
            position: absolute;
            top: 5px;
            right: 5px;
            background: rgba(255, 255, 255, 0.8);
            border: none;
            border-radius: 50%;
            width: 20px;
            height: 20px;
            cursor: pointer;
            display: none;
            align-items: center;
            justify-content: center;
            font-size: 12px;
            color: #666;
            transition: all 0.2s ease;
        }

        .bingo-cell:hover .clear-cell-btn {
            display: flex;
        }

        .clear-cell-btn:hover {
            background: #ff4444;
            color: white;
        }

        @media (max-width: 768px) {
            .bingo-cell {
                min-height: 120px;
                padding: 8px;
            }
            
            .cell-title {
                font-size: 11px;
                min-height: 30px;
            }
            
            .name-input {
                font-size: 11px;
                padding: 4px;
            }
            
            h1 {
                font-size: 1.8em;
            }
            
            .controls {
                flex-direction: column;
            }
            
            button {
                width: 100%;
            }
        }

        .confetti {
            position: fixed;
            width: 10px;
            height: 10px;
            background: #f5576c;
            position: absolute;
            animation: confetti-fall 3s linear;
        }

        @keyframes confetti-fall {
            0% {
                transform: translateY(-100vh) rotate(0deg);
                opacity: 1;
            }
            100% {
                transform: translateY(100vh) rotate(720deg);
                opacity: 0;
            }
        }

        .instructions {
            background: linear-gradient(135deg, #e0c3fc 0%, #8ec5fc 100%);
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            text-align: center;
            color: #333;
        }

        .instructions h3 {
            margin-bottom: 10px;
            color: #764ba2;
        }

        .instructions p {
            font-size: 14px;
            line-height: 1.5;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🎯 人體賓果遊戲 - 填寫名字版 🎯</h1>
        
        <div class="instructions">
            <h3>📝 遊戲說明</h3>
            <p>找到符合條件的兩個人，在對應格子填入他們的名字。當兩個名字都填寫完成，格子會自動變色。完成一條線（橫、直、斜）即獲勝！</p>
        </div>
        
        <div class="stats">
            <div class="stat-item">
                <div class="stat-label">已完成格子</div>
                <div class="stat-value" id="completedCount">0</div>
            </div>
            <div class="stat-item">
                <div class="stat-label">已填寫名字</div>
                <div class="stat-value" id="nameCount">0</div>
            </div>
            <div class="stat-item">
                <div class="stat-label">完成度</div>
                <div class="stat-value" id="progressPercent">0%</div>
            </div>
        </div>
        
        <div class="controls">
            <button class="version-btn active" onclick="loadVersion(1, this)">版本 1</button>
            <button class="version-btn" onclick="loadVersion(2, this)">版本 2</button>
            <button class="version-btn" onclick="loadVersion(3, this)">版本 3</button>
            <button class="reset-btn" onclick="resetBoard()">清空所有</button>
            <button class="export-btn" onclick="exportData()">匯出記錄</button>
        </div>
        
        <div class="bingo-grid" id="bingoGrid"></div>
        
        <div class="name-list" id="nameList" style="display: none;">
            <h3>📋 已收集的名字</h3>
            <div id="nameListContent"></div>
        </div>
    </div>
    
    <div class="win-message" id="winMessage">
        🎉 賓果！你贏了！ 🎉
        <br>
        <button onclick="hideWinMessage()" style="margin-top: 20px;">繼續玩</button>
    </div>

    <script>
        const versions = {
            1: [
                "兩個單身的人", "兩個養狗的人", "兩個有刺青的人", "兩個會樂器的人", "兩個開特斯拉的人",
                "兩個沒看過PT的人", "兩個有參加過馬拉松的人", "兩個2000年後出生的人", "兩個近視超過500度的人", "兩個有上過day1cpt學校的人",
                "兩個支持芋頭放在火鍋裡的人", "兩個有black out過的人", "兩個沒穿過美津濃的人", "兩個養貓的人", "兩個會游泳的人",
                "兩個沒讀過CS或EE的人", "兩個偷渡過有肉的泡麵進美國的人", "兩個有參加過歌唱比賽的人", "兩個另一半不是台灣人的人", "兩個住過東岸跟西岸的人",
                "兩個沒拿過H1B簽證的人", "兩個沒有costco會員卡的人", "兩個滑雪不超過三次的人", "兩個沒看過現場NBA的人", "兩個手機不是iPhone的人"
            ],
            2: [
                "兩個養貓的人", "兩個沒讀過CS或EE的人", "兩個有參加過歌唱比賽的人", "兩個沒拿過H1B簽證的人", "兩個近視超過500度的人",
                "兩個開特斯拉的人", "兩個2000年後出生的人", "兩個沒有costco會員卡的人", "兩個有刺青的人", "兩個偷渡過有肉的泡麵進美國的人",
                "兩個會游泳的人", "兩個另一半不是台灣人的人", "兩個沒穿過美津濃的人", "兩個有black out過的人", "兩個單身的人",
                "兩個住過東岸跟西岸的人", "兩個滑雪不超過三次的人", "兩個養狗的人", "兩個有上過day1cpt學校的人", "兩個會樂器的人",
                "兩個有參加過馬拉松的人", "兩個手機不是iPhone的人", "兩個支持芋頭放在火鍋裡的人", "兩個沒看過PT的人", "兩個沒看過現場NBA的人"
            ],
            3: [
                "兩個手機不是iPhone的人", "兩個有black out過的人", "兩個會樂器的人", "兩個養狗的人", "兩個沒看過現場NBA的人",
                "兩個有參加過馬拉松的人", "兩個支持芋頭放在火鍋裡的人", "兩個單身的人", "兩個沒拿過H1B簽證的人", "兩個另一半不是台灣人的人",
                "兩個有刺青的人", "兩個沒看過PT的人", "兩個沒穿過美津濃的人", "兩個2000年後出生的人", "兩個有參加過歌唱比賽的人",
                "兩個滑雪不超過三次的人", "兩個養貓的人", "兩個近視超過500度的人", "兩個沒有costco會員卡的人", "兩個偷渡過有肉的泡麵進美國的人",
                "兩個會游泳的人", "兩個開特斯拉的人", "兩個住過東岸跟西岸的人", "兩個有上過day1cpt學校的人", "兩個沒讀過CS或EE的人"
            ]
        };

        let currentVersion = 1;
        let cellData = {};

        function loadVersion(version, btn) {
            if (Object.keys(cellData).length > 0) {
                if (!confirm('切換版本會清空所有已填寫的名字，確定要繼續嗎？')) {
                    return;
                }
            }
            
            currentVersion = version;
            cellData = {};
            
            // Update active button
            document.querySelectorAll('.version-btn').forEach(b => b.classList.remove('active'));
            btn.classList.add('active');
            
            // Load grid
            const grid = document.getElementById('bingoGrid');
            grid.innerHTML = '';
            
            versions[version].forEach((item, index) => {
                const cell = document.createElement('div');
                cell.className = 'bingo-cell';
                cell.dataset.index = index;
                
                // Clear button
                const clearBtn = document.createElement('button');
                clearBtn.className = 'clear-cell-btn';
                clearBtn.innerHTML = '×';
                clearBtn.onclick = (e) => {
                    e.stopPropagation();
                    clearCell(index);
                };
                
                // Title
                const title = document.createElement('div');
                title.className = 'cell-title';
                title.textContent = item;
                
                // Name inputs container
                const nameInputs = document.createElement('div');
                nameInputs.className = 'name-inputs';
                
                // Create two input fields
                for (let i = 0; i < 2; i++) {
                    const input = document.createElement('input');
                    input.className = 'name-input';
                    input.type = 'text';
                    input.placeholder = `名字 ${i + 1}`;
                    input.dataset.cellIndex = index;
                    input.dataset.nameIndex = i;
                    input.oninput = () => handleInputChange(index, i, input);
                    nameInputs.appendChild(input);
                }
                
                cell.appendChild(clearBtn);
                cell.appendChild(title);
                cell.appendChild(nameInputs);
                grid.appendChild(cell);
            });
            
            updateStats();
            updateNameList();
        }

        function handleInputChange(cellIndex, nameIndex, input) {
            if (!cellData[cellIndex]) {
                cellData[cellIndex] = {
                    names: ['', ''],
                    title: versions[currentVersion][cellIndex]
                };
            }
            
            cellData[cellIndex].names[nameIndex] = input.value.trim();
            
            // Update visual state
            if (input.value.trim()) {
                input.classList.add('filled');
            } else {
                input.classList.remove('filled');
            }
            
            // Check if both names are filled
            const cell = document.querySelector(`.bingo-cell[data-index="${cellIndex}"]`);
            if (cellData[cellIndex].names[0] && cellData[cellIndex].names[1]) {
                cell.classList.add('completed');
            } else {
                cell.classList.remove('completed');
            }
            
            updateStats();
            updateNameList();
            checkWin();
            
            // Auto-save to localStorage
            saveToLocalStorage();
        }

        function clearCell(cellIndex) {
            delete cellData[cellIndex];
            
            const cell = document.querySelector(`.bingo-cell[data-index="${cellIndex}"]`);
            cell.classList.remove('completed');
            
            const inputs = cell.querySelectorAll('.name-input');
            inputs.forEach(input => {
                input.value = '';
                input.classList.remove('filled');
            });
            
            updateStats();
            updateNameList();
            saveToLocalStorage();
        }

        function updateStats() {
            let completedCount = 0;
            let nameCount = 0;
            
            Object.values(cellData).forEach(data => {
                if (data.names[0] && data.names[1]) {
                    completedCount++;
                }
                if (data.names[0]) nameCount++;
                if (data.names[1]) nameCount++;
            });
            
            document.getElementById('completedCount').textContent = completedCount;
            document.getElementById('nameCount').textContent = nameCount;
            document.getElementById('progressPercent').textContent = Math.round((completedCount / 25) * 100) + '%';
        }

        function updateNameList() {
            const nameListContainer = document.getElementById('nameList');
            const nameListContent = document.getElementById('nameListContent');
            
            if (Object.keys(cellData).length === 0) {
                nameListContainer.style.display = 'none';
                return;
            }
            
            nameListContainer.style.display = 'block';
            nameListContent.innerHTML = '';
            
            Object.entries(cellData).forEach(([index, data]) => {
                if (data.names[0] || data.names[1]) {
                    const entry = document.createElement('div');
                    entry.className = 'name-entry';
                    
                    const nameText = data.names.filter(n => n).join(', ') || '(未完成)';
                    entry.innerHTML = `
                        <div>
                            <strong>${data.title}:</strong>
                            ${nameText}
                        </div>
                    `;
                    
                    nameListContent.appendChild(entry);
                }
            });
        }

        function checkWin() {
            const winPatterns = [
                // Horizontal
                [0, 1, 2, 3, 4],
                [5, 6, 7, 8, 9],
                [10, 11, 12, 13, 14],
                [15, 16, 17, 18, 19],
                [20, 21, 22, 23, 24],
                // Vertical
                [0, 5, 10, 15, 20],
                [1, 6, 11, 16, 21],
                [2, 7, 12, 17, 22],
                [3, 8, 13, 18, 23],
                [4, 9, 14, 19, 24],
                // Diagonal
                [0, 6, 12, 18, 24],
                [4, 8, 12, 16, 20]
            ];

            for (const pattern of winPatterns) {
                if (pattern.every(index => 
                    cellData[index] && 
                    cellData[index].names[0] && 
                    cellData[index].names[1]
                )) {
                    showWinMessage();
                    createConfetti();
                    return;
                }
            }
        }

        function showWinMessage() {
            document.getElementById('winMessage').classList.add('show');
        }

        function hideWinMessage() {
            document.getElementById('winMessage').classList.remove('show');
        }

        function resetBoard() {
            if (Object.keys(cellData).length > 0) {
                if (!confirm('確定要清空所有名字嗎？')) {
                    return;
                }
            }
            
            cellData = {};
            document.querySelectorAll('.bingo-cell').forEach(cell => {
                cell.classList.remove('completed');
                cell.querySelectorAll('.name-input').forEach(input => {
                    input.value = '';
                    input.classList.remove('filled');
                });
            });
            
            updateStats();
            updateNameList();
            hideWinMessage();
            localStorage.removeItem('bingoData');
        }

        function exportData() {
            let exportText = `人體賓果遊戲記錄 - 版本${currentVersion}\n`;
            exportText += `日期: ${new Date().toLocaleDateString('zh-TW')}\n\n`;
            
            Object.entries(cellData).forEach(([index, data]) => {
                if (data.names[0] || data.names[1]) {
                    exportText += `${data.title}:\n`;
                    if (data.names[0]) exportText += `  - ${data.names[0]}\n`;
                    if (data.names[1]) exportText += `  - ${data.names[1]}\n`;
                    exportText += '\n';
                }
            });
            
            // Create download
            const blob = new Blob([exportText], { type: 'text/plain;charset=utf-8' });
            const url = URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = `人體賓果記錄_${new Date().getTime()}.txt`;
            a.click();
            URL.revokeObjectURL(url);
        }

        function saveToLocalStorage() {
            const saveData = {
                version: currentVersion,
                cellData: cellData
            };
            localStorage.setItem('bingoData', JSON.stringify(saveData));
        }

        function loadFromLocalStorage() {
            const saved = localStorage.getItem('bingoData');
            if (saved) {
                const data = JSON.parse(saved);
                if (data.version) {
                    currentVersion = data.version;
                    cellData = data.cellData || {};
                    
                    // Load the correct version
                    const versionBtn = document.querySelectorAll('.version-btn')[data.version - 1];
                    loadVersion(data.version, versionBtn);
                    
                    // Restore input values
                    Object.entries(cellData).forEach(([index, data]) => {
                        const cell = document.querySelector(`.bingo-cell[data-index="${index}"]`);
                        if (cell) {
                            const inputs = cell.querySelectorAll('.name-input');
                            inputs.forEach((input, i) => {
                                if (data.names[i]) {
                                    input.value = data.names[i];
                                    input.classList.add('filled');
                                }
                            });
                            
                            if (data.names[0] && data.names[1]) {
                                cell.classList.add('completed');
                            }
                        }
                    });
                    
                    updateStats();
                    updateNameList();
                }
            }
        }

        function createConfetti() {
            const colors = ['#f5576c', '#f093fb', '#667eea', '#764ba2', '#fee140'];
            for (let i = 0; i < 50; i++) {
                setTimeout(() => {
                    const confetti = document.createElement('div');
                    confetti.className = 'confetti';
                    confetti.style.left = Math.random() * 100 + '%';
                    confetti.style.background = colors[Math.floor(Math.random() * colors.length)];
                    confetti.style.animationDelay = Math.random() * 0.5 + 's';
                    document.body.appendChild(confetti);
                    
                    setTimeout(() => confetti.remove(), 3000);
                }, i * 30);
            }
        }

        // Initialize
        window.onload = () => {
            const saved = localStorage.getItem('bingoData');
            if (saved) {
                loadFromLocalStorage();
            } else {
                loadVersion(1, document.querySelector('.version-btn'));
            }
        };
    </script>
</body>
</html>

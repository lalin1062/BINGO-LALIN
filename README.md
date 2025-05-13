<!DOCTYPE html>
<html lang="th">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>เกมบิงโกการเปรียบเทียบจำนวน</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>เกมบิงโกการเปรียบเทียบจำนวน</h1>
    <p>คลิกเพื่อทำเครื่องหมายในช่องที่ถูกต้อง!</p>
    
    <div class="bingo-card" id="bingo-card">
        <!-- กระดานบิงโกจะถูกสร้างโดย JavaScript -->
    </div>
    
    <div class="question-box">
        <p id="question">คำถามจะขึ้นที่นี่</p>
        <button onclick="generateQuestion()">ถามคำถามใหม่</button>
    </div>

    <script src="script.js"></script>
</body>
</html>
/* style.css */
body {
    font-family: 'Arial', sans-serif;
    text-align: center;
    background-color: #f3f3f3;
    margin: 0;
    padding: 0;
}

h1 {
    color: #4CAF50;
}

.bingo-card {
    display: grid;
    grid-template-columns: repeat(5, 1fr);
    grid-template-rows: repeat(5, 1fr);
    gap: 5px;
    margin: 20px auto;
    width: 50%;
    max-width: 500px;
}

.bingo-card div {
    background-color: #e0e0e0;
    padding: 20px;
    font-size: 18px;
    cursor: pointer;
    text-align: center;
    border: 1px solid #ccc;
}

.bingo-card div.clicked {
    background-color: #4CAF50;
    color: white;
}

.question-box {
    margin-top: 20px;
    font-size: 20px;
}

button {
    padding: 10px 20px;
    background-color: #4CAF50;
    color: white;
    border: none;
    cursor: pointer;
    font-size: 16px;
}

button:hover {
    background-color: #45a049;
}
// script.js

// ตัวแปรสำหรับคำถามและตัวเลขที่ใช้
const questions = [
    { question: "เลือกจำนวนที่มีหลักร้อยเป็น 3", answer: [300, 350, 399] },
    { question: "เปรียบเทียบ 213 กับ 450: ตัวใดมากกว่า?", answer: [450] },
    { question: "เลือกจำนวนคู่ระหว่าง 200 ถึง 300", answer: [200, 202, 204, 206] },
    { question: "เลือกจำนวนคี่ระหว่าง 300 ถึง 400", answer: [301, 303, 305] },
    { question: "เลือกจำนวนที่มีหลักสิบเป็น 4", answer: [40, 140, 240] }
];

// สุ่มคำถาม
function generateQuestion() {
    const randomIndex = Math.floor(Math.random() * questions.length);
    const selectedQuestion = questions[randomIndex];

    // แสดงคำถาม
    document.getElementById('question').innerText = selectedQuestion.question;

    // สุ่มตัวเลขที่ใช้ในกระดานบิงโก
    createBingoCard(selectedQuestion.answer);
}

// สร้างกระดานบิงโก
function createBingoCard(correctAnswers) {
    const bingoCard = document.getElementById('bingo-card');
    bingoCard.innerHTML = ''; // เคลียร์กระดานเก่า

    // สร้างตัวเลขสำหรับกระดานบิงโก
    let numbers = [];
    while (numbers.length < 25) {
        let num = Math.floor(Math.random() * 1000) + 1;
        if (!numbers.includes(num)) {
            numbers.push(num);
        }
    }

    // สร้างช่องบนกระดานบิงโก
    numbers.forEach((number, index) => {
        const div = document.createElement('div');
        div.innerText = number;
        div.onclick = () => handleCellClick(div, number, correctAnswers);
        bingoCard.appendChild(div);
    });
}

// ฟังก์ชันเมื่อคลิกที่ช่อง
function handleCellClick(cell, number, correctAnswers) {
    const question = document.getElementById('question').innerText;

    // ตรวจสอบว่าคำตอบถูกต้องหรือไม่
    if (correctAnswers.includes(number)) {
        cell.classList.add('clicked');
    } else {
        alert('คำตอบไม่ถูกต้อง!');
    }
}

// เริ่มต้นเกม
generateQuestion();

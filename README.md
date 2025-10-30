<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Vocabulary Game: Expressions & Modern Terms</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #ff6b6b 0%, #ffa8a8 100%);
            min-height: 100vh;
            padding: 20px;
            color: #2c3e50;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            max-width: 1000px;
            width: 100%;
            background: white;
            border-radius: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #ff6b6b, #ffa8a8);
            color: white;
            padding: 30px;
            text-align: center;
            position: relative;
        }

        .header h1 {
            font-size: 2.2em;
            margin-bottom: 10px;
            position: relative;
            z-index: 1;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        .header p {
            font-size: 1.1em;
            opacity: 0.9;
            position: relative;
            z-index: 1;
        }

        .nav-buttons {
            display: flex;
            justify-content: center;
            gap: 10px;
            padding: 20px;
            background: #f8f9fa;
            flex-wrap: wrap;
        }

        .nav-btn {
            padding: 12px 20px;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            font-size: 15px;
            font-weight: bold;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }

        .nav-btn.active {
            background: linear-gradient(135deg, #ff6b6b, #ffa8a8);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255, 107, 107, 0.4);
        }

        .nav-btn:not(.active) {
            background: white;
            color: #666;
        }

        .nav-btn:hover:not(.active) {
            background: #e9ecef;
            transform: translateY(-1px);
        }

        .game-section {
            display: none;
            padding: 25px;
            min-height: 400px;
        }

        .game-section.active {
            display: block;
            animation: fadeIn 0.5s ease-in;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .word-bank {
            background: linear-gradient(135deg, #fff5f5, #ffecec);
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 20px;
            border: 2px solid #ff6b6b;
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.2);
        }

        .word-bank h3 {
            color: #ff6b6b;
            margin-bottom: 15px;
            text-align: center;
            font-size: 1.3em;
        }

        .word-options {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            justify-content: center;
        }

        .word-option {
            background: linear-gradient(135deg, #ff6b6b, #ffa8a8);
            color: white;
            padding: 8px 16px;
            border-radius: 20px;
            font-weight: bold;
            font-size: 14px;
            box-shadow: 0 3px 10px rgba(255, 107, 107, 0.3);
            transition: all 0.3s ease;
            cursor: default;
            text-align: center;
        }

        .word-option:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(255, 107, 107, 0.4);
        }

        .question {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 15px;
            margin-bottom: 15px;
            border-left: 5px solid #ff6b6b;
            box-shadow: 0 4px 15px rgba(0,0,0,0.05);
        }

        .question h3 {
            color: #ff6b6b;
            margin-bottom: 12px;
            font-size: 1.2em;
        }

        .fill-blank {
            background: #fff;
            border: 2px solid #ddd;
            border-radius: 8px;
            padding: 8px 12px;
            font-size: 15px;
            margin: 0 5px;
            min-width: 140px;
            transition: border-color 0.3s ease;
        }

        .fill-blank.correct {
            border-color: #4CAF50;
            background: #e8f5e8;
        }

        .fill-blank.incorrect {
            border-color: #f44336;
            background: #ffeaea;
        }

        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 12px;
            margin-top: 12px;
        }

        .option {
            padding: 12px 18px;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
            font-size: 14px;
        }

        .option:hover {
            border-color: #ff6b6b;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.2);
        }

        .option.selected {
            background: #ff6b6b;
            color: white;
            border-color: #ff6b6b;
        }

        .option.correct {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
        }

        .option.incorrect {
            background: #f44336;
            color: white;
            border-color: #f44336;
        }

        .matching-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
            margin-top: 20px;
        }

        .match-column h4 {
            text-align: center;
            margin-bottom: 15px;
            color: #ff6b6b;
            font-size: 1.1em;
        }

        .match-item {
            padding: 12px;
            margin: 6px 0;
            border: 2px solid #ddd;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            background: white;
            text-align: center;
            font-weight: 500;
            font-size: 14px;
        }

        .match-item:hover {
            border-color: #ff6b6b;
            transform: translateY(-1px);
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.2);
        }

        .match-item.selected {
            background: #ffecec;
            border-color: #ff6b6b;
        }

        .match-item.matched {
            background: #4CAF50;
            color: white;
            border-color: #4CAF50;
            cursor: default;
        }

        .check-btn {
            background: linear-gradient(135deg, #ff6b6b, #ffa8a8);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 15px;
            font-weight: bold;
            margin: 15px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
        }

        .check-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(255, 107, 107, 0.4);
        }

        .reset-btn {
            background: linear-gradient(135deg, #f44336, #ff7961);
            color: white;
            border: none;
            padding: 12px 25px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 15px;
            font-weight: bold;
            margin: 10px auto;
            display: block;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(244, 67, 54, 0.3);
        }

        .reset-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(244, 67, 54, 0.4);
        }

        .feedback {
            margin-top: 12px;
            padding: 12px;
            border-radius: 10px;
            font-weight: bold;
            text-align: center;
            animation: slideIn 0.3s ease;
            font-size: 14px;
        }

        @keyframes slideIn {
            from { transform: translateX(-20px); opacity: 0; }
            to { transform: translateX(0); opacity: 1; }
        }

        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 1px solid #c3e6cb;
        }

        .feedback.incorrect {
            background: #f8d7da;
            color: #721c24;
            border: 1px solid #f5c6cb;
        }

        .score {
            position: fixed;
            top: 20px;
            right: 20px;
            background: linear-gradient(135deg, #ff6b6b, #ffa8a8);
            color: white;
            padding: 12px 18px;
            border-radius: 25px;
            font-weight: bold;
            box-shadow: 0 4px 15px rgba(255, 107, 107, 0.3);
            z-index: 1000;
        }

        .icon {
            font-size: 22px;
            margin-right: 8px;
            vertical-align: middle;
        }

        /* Vocabulary List Styles */
        .vocabulary-list {
            padding: 15px;
        }

        .vocabulary-item {
            margin-bottom: 20px;
            padding: 18px;
            border-radius: 10px;
            background: #f8f9fa;
            box-shadow: 0 4px 10px rgba(0,0,0,0.05);
        }

        .vocabulary-item h3 {
            color: #ff6b6b;
            margin-bottom: 8px;
            font-size: 1.3em;
            border-bottom: 2px solid #ff6b6b;
            padding-bottom: 6px;
        }

        .vocabulary-item p {
            margin-bottom: 6px;
            line-height: 1.5;
            font-size: 14px;
        }

        .example {
            font-style: italic;
            color: #555;
            padding-left: 12px;
            border-left: 3px solid #ff6b6b;
            margin-top: 8px;
            font-size: 13px;
        }

        @media (max-width: 768px) {
            .matching-container {
                grid-template-columns: 1fr;
                gap: 15px;
            }
            
            .nav-buttons {
                flex-direction: column;
                align-items: center;
            }
            
            .nav-btn {
                width: 180px;
                font-size: 14px;
            }
            
            .score {
                position: static;
                margin: 15px auto;
                display: block;
                width: fit-content;
            }
            
            .header h1 {
                font-size: 1.8em;
            }
        }
    </style>
</head>
<body>
    <div class="score">Score: <span id="score">0</span>/12</div>
    
    <div class="container">
        <div class="header">
            <h1><i class="fas fa-book icon"></i> Vocabulary Game: Expressions & Modern Terms</h1>
            <p>Test your knowledge of these English expressions!</p>
        </div>

        <div class="nav-buttons">
            <button class="nav-btn active" onclick="showSection('vocabulary')">Vocabulary List</button>
            <button class="nav-btn" onclick="showSection('fill-gaps')">Fill in the Gaps</button>
            <button class="nav-btn" onclick="showSection('matching')">Match Definitions</button>
            <button class="nav-btn" onclick="showSection('multiple-choice')">Multiple Choice</button>
        </div>

        <!-- Vocabulary List Section -->
        <div id="vocabulary" class="game-section active">
            <h2 style="text-align: center; margin-bottom: 20px; color: #ff6b6b;">Vocabulary Explanations</h2>
            
            <div class="vocabulary-list">
                <div class="vocabulary-item">
                    <h3>factor in</h3>
                    <p><strong>Definition:</strong> To include something as a relevant element when making a decision or calculation.</p>
                    <p><strong>Usage:</strong> Common in planning, analysis, and decision-making contexts.</p>
                    <p class="example"><strong>Example:</strong> "When planning the budget, we need to factor in unexpected expenses."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>upheaval</h3>
                    <p><strong>Definition:</strong> A violent or sudden change or disruption to something.</p>
                    <p><strong>Usage:</strong> Often used to describe major changes in society, organizations, or personal life.</p>
                    <p class="example"><strong>Example:</strong> "The company went through a major upheaval when the new CEO took over."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>figure out</h3>
                    <p><strong>Definition:</strong> To understand or solve something; to find the answer to a problem.</p>
                    <p><strong>Usage:</strong> Used when working through problems or understanding complex situations.</p>
                    <p class="example"><strong>Example:</strong> "I need to figure out how to fix this computer issue."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>retirees</h3>
                    <p><strong>Definition:</strong> People who have stopped working, usually after reaching a certain age.</p>
                    <p><strong>Usage:</strong> Refers to people who have retired from their careers.</p>
                    <p class="example"><strong>Example:</strong> "Many retirees move to warmer climates for their retirement years."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>that sucks</h3>
                    <p><strong>Definition:</strong> An informal expression meaning something is very bad, disappointing, or unfortunate.</p>
                    <p><strong>Usage:</strong> Casual expression of disappointment or sympathy.</p>
                    <p class="example"><strong>Example:</strong> "You have to work on your birthday? That sucks!"</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>either way</h3>
                    <p><strong>Definition:</strong> Whichever of two given alternatives is the case; in any case.</p>
                    <p><strong>Usage:</strong> Used when the outcome will be the same regardless of the choice.</p>
                    <p class="example"><strong>Example:</strong> "We can take the highway or the back roads - either way, we'll get there on time."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>no end in sight</h3>
                    <p><strong>Definition:</strong> No indication that something will stop or finish soon.</p>
                    <p><strong>Usage:</strong> Used for situations that seem like they will continue indefinitely.</p>
                    <p class="example"><strong>Example:</strong> "The construction noise has been going on for months with no end in sight."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>it is a given</h3>
                    <p><strong>Definition:</strong> Something that is certain or accepted as true without question.</p>
                    <p><strong>Usage:</strong> Used for assumptions that everyone accepts as true.</p>
                    <p class="example"><strong>Example:</strong> "It's a given that the team will make the playoffs this year."</p>
                </div>
                
                <div class="vocabulary-item">
                    <h3>blow my mind</h3>
                    <p><strong>Definition:</strong> To greatly surprise or astonish someone; to be extremely impressive.</p>
                    <p><strong>Usage:</strong> Informal expression for something that is amazing or hard to believe.</p>
                    <p class="example"><strong>Example:</strong> "The special effects in that movie completely blew my mind!"</p>
                </div>
            </div>
        </div>

        <!-- Fill in the Gaps Section -->
        <div id="fill-gaps" class="game-section">
            <div class="word-bank">
                <h3><i class="fas fa-list-ul icon"></i> Word Bank - Choose from these expressions:</h3>
                <div class="word-options">
                    <span class="word-option">factor in</span>
                    <span class="word-option">upheaval</span>
                    <span class="word-option">figure out</span>
                    <span class="word-option">retirees</span>
                    <span class="word-option">that sucks</span>
                    <span class="word-option">either way</span>
                    <span class="word-option">no end in sight</span>
                    <span class="word-option">it is a given</span>
                    <span class="word-option">blow my mind</span>
                </div>
            </div>

            <div id="fill-gaps-container">
                <!-- Sentences will be dynamically inserted here -->
            </div>

            <button class="check-btn" onclick="checkFillBlanks()">Check Answers</button>
            <button class="reset-btn" onclick="resetFillBlanks()">Reset Answers</button>
        </div>

        <!-- Matching Section -->
        <div id="matching" class="game-section">
            <h2 style="text-align: center; margin-bottom: 20px; color: #ff6b6b;">Match the expressions with their definitions</h2>
            <div class="matching-container">
                <div class="match-column">
                    <h4>Vocabulary Expressions</h4>
                    <div class="match-item" data-word="factor in" onclick="selectMatch(this)">factor in</div>
                    <div class="match-item" data-word="upheaval" onclick="selectMatch(this)">upheaval</div>
                    <div class="match-item" data-word="figure out" onclick="selectMatch(this)">figure out</div>
                    <div class="match-item" data-word="retirees" onclick="selectMatch(this)">retirees</div>
                    <div class="match-item" data-word="that sucks" onclick="selectMatch(this)">that sucks</div>
                    <div class="match-item" data-word="either way" onclick="selectMatch(this)">either way</div>
                    <div class="match-item" data-word="no end in sight" onclick="selectMatch(this)">no end in sight</div>
                    <div class="match-item" data-word="it is a given" onclick="selectMatch(this)">it is a given</div>
                    <div class="match-item" data-word="blow my mind" onclick="selectMatch(this)">blow my mind</div>
                </div>
                <div class="match-column">
                    <h4>Definitions</h4>
                    <div id="meanings-container">
                        <!-- Meanings will be dynamically inserted here -->
                    </div>
                </div>
            </div>
            <div class="feedback" id="matching-feedback" style="display: none;"></div>
            <button class="check-btn" onclick="checkMatching()">Check Matching</button>
            <button class="reset-btn" onclick="resetMatching()">Reset Matching</button>
        </div>

        <!-- Multiple Choice Section -->
        <div id="multiple-choice" class="game-section">
            <div class="question">
                <h3>Question 1: What does "factor in" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To ignore something important</div>
                    <div class="option" onclick="selectOption(this, true)">To include as a relevant element in decision-making</div>
                    <div class="option" onclick="selectOption(this, false)">To remove something from consideration</div>
                    <div class="option" onclick="selectOption(this, false)">To calculate mathematical factors</div>
                </div>
                <div class="feedback" id="mc-feedback-1" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 2: What is an "upheaval"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">A small, gradual change</div>
                    <div class="option" onclick="selectOption(this, true)">A violent or sudden change or disruption</div>
                    <div class="option" onclick="selectOption(this, false)">A peaceful transition</div>
                    <div class="option" onclick="selectOption(this, false)">A routine procedure</div>
                </div>
                <div class="feedback" id="mc-feedback-2" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 3: What does "figure out" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To ignore a problem</div>
                    <div class="option" onclick="selectOption(this, true)">To understand or solve something</div>
                    <div class="option" onclick="selectOption(this, false)">To draw a picture</div>
                    <div class="option" onclick="selectOption(this, false)">To calculate numbers</div>
                </div>
                <div class="feedback" id="mc-feedback-3" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 4: Who are "retirees"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Young people starting their careers</div>
                    <div class="option" onclick="selectOption(this, true)">People who have stopped working after reaching retirement age</div>
                    <div class="option" onclick="selectOption(this, false)">Students in university</div>
                    <div class="option" onclick="selectOption(this, false)">People between jobs</div>
                </div>
                <div class="feedback" id="mc-feedback-4" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 5: When would you say "that sucks"?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">When something is excellent</div>
                    <div class="option" onclick="selectOption(this, true)">When something is disappointing or unfortunate</div>
                    <div class="option" onclick="selectOption(this, false)">When you're confused</div>
                    <div class="option" onclick="selectOption(this, false)">When you're happy</div>
                </div>
                <div class="feedback" id="mc-feedback-5" style="display: none;"></div>
            </div>

            <div class="question">
                <h3>Question 6: What does "either way" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Only one option is acceptable</div>
                    <div class="option" onclick="selectOption(this, true)">Whichever alternative is chosen</div>
                    <div class="option" onclick="selectOption(this, false)">Neither option is good</div>
                    <div class="option" onclick="selectOption(this, false)">Both options are impossible</div>
                </div>
                <div class="feedback" id="mc-feedback-6" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 7: What does "no end in sight" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Something will end very soon</div>
                    <div class="option" onclick="selectOption(this, true)">No indication that something will stop soon</div>
                    <div class="option" onclick="selectOption(this, false)">The end is clearly visible</div>
                    <div class="option" onclick="selectOption(this, false)">Something has already ended</div>
                </div>
                <div class="feedback" id="mc-feedback-7" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 8: What does "it is a given" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">Something is questionable</div>
                    <div class="option" onclick="selectOption(this, true)">Something is certain or accepted as true</div>
                    <div class="option" onclick="selectOption(this, false)">Something was given as a gift</div>
                    <div class="option" onclick="selectOption(this, false)">Something is optional</div>
                </div>
                <div class="feedback" id="mc-feedback-8" style="display: none;"></div>
            </div>
            
            <div class="question">
                <h3>Question 9: What does "blow my mind" mean?</h3>
                <div class="options">
                    <div class="option" onclick="selectOption(this, false)">To make someone angry</div>
                    <div class="option" onclick="selectOption(this, true)">To greatly surprise or astonish someone</div>
                    <div class="option" onclick="selectOption(this, false)">To confuse someone</div>
                    <div class="option" onclick="selectOption(this, false)">To bore someone</div>
                </div>
                <div class="feedback" id="mc-feedback-9" style="display: none;"></div>
            </div>
            
            <button class="reset-btn" onclick="resetMultipleChoice()">Reset Answers</button>
        </div>
    </div>

    <script>
        let score = 0;
        let selectedWord = null;
        let selectedMeaning = null;
        let matchedPairs = [];
        
        // Track correct answers for each section
        let fillBlanksCorrect = 0;
        let matchingCorrect = 0;
        let multipleChoiceCorrect = 0;
        
        // Definitions for the matching game
        const definitions = [
            { meaning: "factor in", text: "To include as relevant in decision-making" },
            { meaning: "upheaval", text: "A violent or sudden change or disruption" },
            { meaning: "figure out", text: "To understand or solve something" },
            { meaning: "retirees", text: "People who have stopped working" },
            { meaning: "that sucks", text: "Expression for something disappointing" },
            { meaning: "either way", text: "Whichever alternative is chosen" },
            { meaning: "no end in sight", text: "No indication something will stop soon" },
            { meaning: "it is a given", text: "Something certain or accepted as true" },
            { meaning: "blow my mind", text: "To greatly surprise or astonish" }
        ];

        // Sentences for the fill-in-the-blanks game
        const sentences = [
            { text: "When planning the budget, we need to <input type='text' class='fill-blank' data-answer='factor in' placeholder='answer'> unexpected expenses.", answer: "factor in" },
            { text: "The company went through a major <input type='text' class='fill-blank' data-answer='upheaval' placeholder='answer'> when the new CEO took over.", answer: "upheaval" },
            { text: "I need to <input type='text' class='fill-blank' data-answer='figure out' placeholder='answer'> how to fix this computer issue.", answer: "figure out" },
            { text: "Many <input type='text' class='fill-blank' data-answer='retirees' placeholder='answer'> move to warmer climates for their retirement years.", answer: "retirees" },
            { text: "You have to work on your birthday? <input type='text' class='fill-blank' data-answer='that sucks' placeholder='answer'>!", answer: "that sucks" },
            { text: "We can take the highway or the back roads - <input type='text' class='fill-blank' data-answer='either way' placeholder='answer'>, we'll get there on time.", answer: "either way" },
            { text: "The construction noise has been going on for months with <input type='text' class='fill-blank' data-answer='no end in sight' placeholder='answer'>.", answer: "no end in sight" },
            { text: "It's <input type='text' class='fill-blank' data-answer='a given' placeholder='answer'> that the team will make the playoffs this year.", answer: "a given" },
            { text: "The special effects in that movie completely <input type='text' class='fill-blank' data-answer='blew my mind' placeholder='answer'>!", answer: "blew my mind" },
            { text: "Before making a decision, we should <input type='text' class='fill-blank' data-answer='factor in' placeholder='answer'> all the possible risks.", answer: "factor in" }
        ];

        // Function to shuffle array (Fisher-Yates algorithm)
        function shuffleArray(array) {
            for (let i = array.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [array[i], array[j]] = [array[j], array[i]];
            }
            return array;
        }

        // Initialize the fill-in-the-blanks game with shuffled sentences
        function initFillBlanks() {
            const container = document.getElementById('fill-gaps-container');
            container.innerHTML = '';
            
            // Shuffle the sentences
            const shuffledSentences = shuffleArray([...sentences]);
            
            // Create and append the sentence elements
            shuffledSentences.forEach((sentence, index) => {
                const div = document.createElement('div');
                div.className = 'question';
                div.innerHTML = `
                    <h3>Question ${index + 1}:</h3>
                    <p>${sentence.text}</p>
                    <div class="feedback" id="feedback-${index + 1}" style="display: none;"></div>
                `;
                container.appendChild(div);
            });
        }

        // Initialize the matching game with shuffled definitions
        function initMatchingGame() {
            const meaningsContainer = document.getElementById('meanings-container');
            meaningsContainer.innerHTML = '';
            
            // Shuffle the definitions
            const shuffledDefinitions = shuffleArray([...definitions]);
            
            // Create and append the definition elements
            shuffledDefinitions.forEach(def => {
                const div = document.createElement('div');
                div.className = 'match-item';
                div.setAttribute('data-meaning', def.meaning);
                div.onclick = function() { selectMatch(this); };
                div.textContent = def.text;
                meaningsContainer.appendChild(div);
            });
        }

        function showSection(sectionId) {
            // Hide all sections
            document.querySelectorAll('.game-section').forEach(section => {
                section.classList.remove('active');
            });
            
            // Remove active class from all buttons
            document.querySelectorAll('.nav-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            
            // Show selected section
            document.getElementById(sectionId).classList.add('active');
            
            // Add active class to clicked button
            event.target.classList.add('active');
            
            // If showing fill-in-the-blanks section, reinitialize with shuffled sentences
            if (sectionId === 'fill-gaps') {
                initFillBlanks();
            }
            
            // If showing matching section, reinitialize with shuffled definitions
            if (sectionId === 'matching') {
                initMatchingGame();
                // Reset matching game state
                document.querySelectorAll('.match-item').forEach(item => {
                    item.classList.remove('selected', 'matched');
                });
                selectedWord = null;
                selectedMeaning = null;
                matchedPairs = [];
                document.getElementById('matching-feedback').style.display = 'none';
            }
            
            // Update score display
            updateScore();
        }

        function checkFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            let correctCount = 0;
            
            blanks.forEach((blank, index) => {
                const userAnswer = blank.value.toLowerCase().trim();
                const correctAnswer = blank.dataset.answer.toLowerCase();
                
                if (userAnswer === correctAnswer) {
                    blank.classList.remove('incorrect');
                    blank.classList.add('correct');
                    correctCount++;
                } else {
                    blank.classList.remove('correct');
                    blank.classList.add('incorrect');
                }
                
                // Show feedback for each question
                const feedback = document.getElementById(`feedback-${index+1}`);
                if (userAnswer === correctAnswer) {
                    feedback.textContent = '✅ Correct!';
                    feedback.className = 'feedback correct';
                } else {
                    feedback.textContent = `❌ Incorrect. The correct answer is: "${blank.dataset.answer}"`;
                    feedback.className = 'feedback incorrect';
                }
                feedback.style.display = 'block';
            });
            
            fillBlanksCorrect = correctCount;
            updateScore();
        }

        function resetFillBlanks() {
            const blanks = document.querySelectorAll('.fill-blank');
            blanks.forEach(blank => {
                blank.value = '';
                blank.classList.remove('correct', 'incorrect');
            });
            
            const feedbacks = document.querySelectorAll('#fill-gaps .feedback');
            feedbacks.forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            fillBlanksCorrect = 0;
            updateScore();
        }

        function selectMatch(element) {
            if (element.classList.contains('matched')) return;
            
            if (element.dataset.word) {
                // Word selected
                if (selectedWord) selectedWord.classList.remove('selected');
                selectedWord = element;
                element.classList.add('selected');
            } else {
                // Meaning selected
                if (selectedMeaning) selectedMeaning.classList.remove('selected');
                selectedMeaning = element;
                element.classList.add('selected');
            }
            
            // Check if we have both word and meaning selected
            if (selectedWord && selectedMeaning) {
                checkMatch();
            }
        }

        function checkMatch() {
            const feedback = document.getElementById('matching-feedback');
            
            if (selectedWord.dataset.word === selectedMeaning.dataset.meaning) {
                // Correct match
                selectedWord.classList.remove('selected');
                selectedWord.classList.add('matched');
                selectedMeaning.classList.remove('selected');
                selectedMeaning.classList.add('matched');
                
                matchedPairs.push(selectedWord.dataset.word);
                
                feedback.textContent = '✅ Correct match!';
                feedback.className = 'feedback correct';
                
                // Check if all matches are complete
                if (matchedPairs.length === definitions.length) {
                    feedback.textContent = '🎉 Congratulations! You matched all terms correctly!';
                }
            } else {
                // Incorrect match
                feedback.textContent = '❌ Incorrect match. Try again.';
                feedback.className = 'feedback incorrect';
            }
            
            feedback.style.display = 'block';
            selectedWord = null;
            selectedMeaning = null;
            
            matchingCorrect = matchedPairs.length;
            updateScore();
        }

        function checkMatching() {
            const allMatches = document.querySelectorAll('.match-item[data-word]');
            let allCorrect = true;
            
            allMatches.forEach(item => {
                if (!item.classList.contains('matched')) {
                    allCorrect = false;
                }
            });
            
            const feedback = document.getElementById('matching-feedback');
            if (allCorrect) {
                feedback.textContent = '🎉 Excellent! All matches are correct!';
                feedback.className = 'feedback correct';
            } else {
                const unmatchedCount = definitions.length - matchedPairs.length;
                feedback.textContent = `You have ${unmatchedCount} unmatched pair${unmatchedCount !== 1 ? 's' : ''}. Keep trying!`;
                feedback.className = 'feedback incorrect';
            }
            feedback.style.display = 'block';
        }

        function resetMatching() {
            document.querySelectorAll('.match-item').forEach(item => {
                item.classList.remove('selected', 'matched');
            });
            
            initMatchingGame();
            
            selectedWord = null;
            selectedMeaning = null;
            matchedPairs = [];
            
            document.getElementById('matching-feedback').style.display = 'none';
            
            matchingCorrect = 0;
            updateScore();
        }

        function selectOption(element, isCorrect) {
            // Remove selection from all options in this question
            const options = element.parentElement.querySelectorAll('.option');
            options.forEach(opt => {
                opt.classList.remove('selected');
                opt.classList.remove('correct');
                opt.classList.remove('incorrect');
            });
            
            // Mark the selected option
            element.classList.add('selected');
            
            const questionNumber = element.closest('.question').querySelector('h3').textContent.match(/\d+/)[0];
            const feedback = document.getElementById(`mc-feedback-${questionNumber}`);
            
            if (isCorrect) {
                element.classList.add('correct');
                feedback.textContent = '✅ Correct!';
                feedback.className = 'feedback correct';
            } else {
                element.classList.add('incorrect');
                feedback.textContent = '❌ Incorrect. Try again.';
                feedback.className = 'feedback incorrect';
                
                // Show the correct answer
                options.forEach(opt => {
                    if (opt.onclick.toString().includes('true')) {
                        opt.classList.add('correct');
                    }
                });
            }
            
            feedback.style.display = 'block';
            
            // Count correct answers in multiple choice
            multipleChoiceCorrect = document.querySelectorAll('#multiple-choice .option.correct.selected').length;
            updateScore();
        }

        function resetMultipleChoice() {
            document.querySelectorAll('#multiple-choice .option').forEach(option => {
                option.classList.remove('selected', 'correct', 'incorrect');
            });
            
            document.querySelectorAll('#multiple-choice .feedback').forEach(feedback => {
                feedback.style.display = 'none';
            });
            
            multipleChoiceCorrect = 0;
            updateScore();
        }

        function updateScore() {
            // Total score
            score = fillBlanksCorrect + matchingCorrect + multipleChoiceCorrect;
            document.getElementById('score').textContent = score;
        }
        
        // Initialize the page
        window.onload = function() {
            initFillBlanks();
            initMatchingGame();
        }
    </script>
</body>
</html>

# Coad-Alph_task2-build-a-calculator
```


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>basic calc</title>
</head>
<body>
    <style>
        *{
             box-sizing: border-box;
              padding: 0;
              margin: 0;
        }
        body{
            display: flex;
            background: linear-gradient(to bottom right,violet,lightblue);
            background-repeat:no-repeat;
            width:100%;
            height:100vh;
            justify-content: center;
            align-items: center;
           
        }

        .calc{
           
            width:400px;
            padding:25px;
            background-color: rgba(0, 0, 0, 0.816);
            border-radius: 30px;
        }
        .display{
            margin-bottom: 20px;
            width: 100%;
            height: 90px;
            padding:25px;
            border-radius: 15px;
            text-align: right;
            border: none;
            font-size: 30px;
        }
        .buttons{
            display: grid;
            grid-template-columns: repeat(4,1fr);
            gap: 10px ; 
        }
        button{
            height:80px;
            border-radius: 20px;
            font-size: 20px;
            color: white;
            background-color: rgba(128, 128, 128, 0.682);
            border:none;
        }
        
        button:hover{
            background-color: gray;
        }
        .operators{
            background-color: orange;
        }
        .operators:hover{
            background-color:rgb(255, 136, 0);
        }
        .clear{
            background-color: rgb(236, 61, 17);
        }
        .clear:hover{
            background-color: rgb(171, 5, 13);
        }
        .equalto{
            background-color: rgb(21, 247, 216);
        }
        .equalto:hover{
            background-color:rgb(4, 148, 121) ;
        }
        .zero{
            grid-column: span 2;
        }

    </style>
    <div class="calc">
        <input type="text" class="display" id="display">
        <div class="buttons">
        <button class="clear" onclick="clearDisplay()">C</button>
        <button onclick="deleteLast()">DEL</button>
        <button onclick="appendValue('%')">%</button>
        <button class="operators" onclick="appendValue('/')">/</button>

        <button onclick="appendValue('7')">7</button>
        <button onclick="appendValue('8')">8</button>
        <button onclick="appendValue('9')">9</button>
        <button class="operators" onclick="appendValue('*')">*</button>
        
        <button onclick="appendValue('4')">4</button>
        <button onclick="appendValue('5')">5</button>
        <button onclick="appendValue('6')">6</button>
        <button class="operators" onclick="appendValue('-')">-</button>

        <button onclick="appendValue('1')">1</button>
        <button onclick="appendValue('2')">2</button>
        <button onclick="appendValue('3')">3</button>
        <button  class="operators" onclick="appendValue('+')">+</button>

        <button class="zero" onclick="appendValue('0')">0</button>
        <button onclick="appendValue('.')">.</button>
        <button class="equalto" onclick="calculate()">=</button>
        </div>
    </div>
</body>

    <script>

        
        const display = document.getElementById("display");


        function appendValue(value) {

            if (display.value === "0" || display.value === "Error") {
                display.value = value;
            } 
            else {
                display.value += value;
            }
        }


        function clearDisplay() {
            display.value = "0";
        }

        function deleteLast() {

            if (display.value.length === 1 || display.value === "Error") {
                display.value = "0";
            } 
            else {
                display.value = display.value.slice(0, -1);
            }
        }


        function calculate() {

            try {

                let expression = display.value;

                
                expression = expression.replace(/(\d+(?:\.\d+)?)%/g, "($1/100)");

                let result = eval(expression);

                if (!isFinite(result)) {
                    display.value = "Error";
                } 
                else {
                    display.value = result;
                }

            } 
            catch (error) {
                display.value = "Error";
            }
        }


        document.addEventListener("keydown", function(event) {

            const key = event.key;

           
            if (key >= "0" && key <= "9") {
                appendValue(key);
            }

            
            else if (
                key === "+" ||
                key === "-" ||
                key === "*" ||
                key === "/" ||
                key === "%"
            ) {
                appendValue(key);
            }

           
            else if (key === ".") {
                appendValue(".");
            }

           
            else if (key === "Enter" || key === "=") {
                calculate();
            }

           
            else if (key === "Backspace") {
                deleteLast();
            }

            
            else if (key === "Escape") {
                clearDisplay();
            }

        });

    </script>

</body>
</html>
```

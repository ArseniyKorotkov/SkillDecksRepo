# 1. File Formats

The application can accept files in the '.txt' and '.csv' formats. <br>
The '.txt' format is applicable if the goal is to make the file a memo with a list of values or if there is no possibility to create a '.csv' file. <br>
The '.csv' format is applicable if the goal is to create a set of decks as simply and quickly as possible. <br>
<br>

# 2. Instruction Application

1. All keywords must be used in the case specified in the instruction.<br>
2. All keywords and symbols highlighted in the instruction with a ',' are used without this auxiliary mark. <br>

# 3. Basics

1. The name of the deck set is the name of the created file.
2. All lines before the first occurrence of the line with the keyword 'PART' at the beginning will be ignored.
3. Basic HTML tags are allowed in the file, except in question answers (they will be read as plain text).
4. To color text in a highlighting color on the theoretical page, use the attribute ' style="color: DEFAULT_APP;" '.

# 4. Special Characters

1. The key symbol '—' is one of the main special characters and is written as follows: <br>
   Press and hold Alt + 0151 on the numeric keypad.
2. The '#' symbol is used as a commenting special character. A line that starts with this symbol will not be processed as a card and serves for adding explanations on the theoretical page.
3. The '$' symbol is used as a commenting special character. A line that starts with this symbol will be processed as a card but will not be included in the explanations on the theoretical page.

# 5. Creating a Deck Set in a '.txt' File

### 1. Creating a Deck

1. To create a new deck, write the keyword 'PART' at the beginning of the line, followed by the deck name separated by '—'. <br>
   Example: PART — Deck Name.
2. All further information in the file until the next occurrence of a line with the keyword 'PART' at the beginning or until the end of the file will belong to the 'Deck Name' deck.

### 2. Creating a Card

1. In the card assignment line, the answer comes first, followed by the question.
2. Each line of the file is considered a card assignment except for lines:<br>
    - with the keyword 'PART' at the beginning
    - with a commenting special character at the beginning (see the 'Special Characters' section)
      Example: answer — question
3. If a line does not have a commenting special character at the beginning and does not contain the '—' symbol, it is not included in the task list and is marked with the warning '<span style="color: red;">! wrong line:</span>', which is visible on the theoretical page. <br>
   If the deck contains at least one wrong line, the theoretical page will display the message 'Have wrong line in deck'.
4. A fragment of the question text enclosed in ',' will be added to the list of auxiliary buttons for the card.

### 2.1. Additional Instructions for the Card

1. Any card can optionally have three additional instructions:
    - auxiliary buttons
    - answer field prefill
    - initial cursor position in the answer field
2. Additional instructions are placed inside an HTML comment at the end of the line using the following keywords:
- BUTTON (for auxiliary buttons)
- PREFILL (for answer field prefill)
- CURSOR (for the initial cursor position in the answer field)
3. After the keyword, an instruction must always be enclosed in curly braces.
4. The special character '\\' escapes any character inside the instructions.
5. To add auxiliary buttons, after the keyword 'BUTTON', enclose the list in curly braces and separate items with commas (spaces will be included in the button text). If this instruction is absent, only auxiliary buttons created from fragments of the question text enclosed in ',' will be shown.<br>
   Example: BUTTON{b1,\\,,\\},b2} will produce buttons:
    - b1
    - ,
    - }
    - b2
6. To prefill the answer field, enclose the text in curly braces after the keyword 'PREFILL'. If this instruction is absent, the answer input field will initially be empty.
7. To set the initial cursor position, enclose a number in curly braces after the keyword 'CURSOR'. If this instruction is absent or if the value cannot be read as a number, the cursor will initially be placed at the end of the text in the answer field.

Example of a card creation line: <br>
answer — question &lt;!--BUTTON{b1,\\,,\\},b2} PREFILL{ans wer} CURSOR{4} --&gt; <br>
The order of keywords does not matter.

# 6. Creating a Deck Set in a '.csv' File

### 1. Creating a Deck

1. '.csv' files are created on the <a href="https://docs.google.com/spreadsheets/">Google Sheets</a> website.
2. To create a new deck, write the keyword 'PART' in the first column and the deck name in the second column of the same row. <br>
3. All further information in the file until the next occurrence of the keyword 'PART' in the first column or until the end of the file will belong to the deck created in the previous rows.

### 2. Creating a Card

1. In the card assignment row, the answer is in the first column, and the question is in the second column.
2. Each row in the file is considered a card assignment except for rows:<br>
    - with the keyword 'PART' in the first column
    - with a commenting special character at the beginning of the first column's text (see the 'Special Characters' section)
3. If a row does not have a commenting special character at the beginning of the first column's text and does not contain text in the second column, it is not included in the task list and is marked with the warning '<span style="color: red;">! wrong line:</span>', which is visible on the theoretical page. <br>
   If the deck contains at least one wrong line, the theoretical page will display the message 'Have wrong line in deck'.
4. A fragment of the second column's text enclosed in ',' will be added to the list of auxiliary buttons for the card.

### 2.1. Additional Instructions for the Card

1. Any card can optionally have three additional instructions:
    - answer field prefill
    - initial cursor position in the answer field
    - auxiliary buttons
2. To prefill the answer field, enclose the text in the third column of the card row. If this instruction is absent, the answer input field will initially be empty.
3. To set the initial cursor position, enclose a number in the fourth column of the card row. If this instruction is absent or if the value cannot be read as a number, the cursor will initially be placed at the end of the text in the answer field.
4. To add auxiliary buttons, starting from the fifth column of the card row, enter the text for the buttons in each column separately. If this instruction is absent, only auxiliary buttons created from fragments of the question text enclosed in ',' will be shown.


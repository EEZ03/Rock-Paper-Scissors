import random

#Lists to have multiple answers equal the same output.
rock = ['ROCK','Rock','rock','r','1']
paper = ['PAPER','Paper','paper','p','2']
scissors = ['SCISSORS','Scissors','scissors','s','3']
rps = ['Rock','Paper','Scissors']
quit = ['QUIT','Quit','quit','q']
restart = ['YES','Yes','yes','y']

#score
s1 = 0
s2 = 0

def text():
    """Simple Text."""
    print('P1-' + str(s1) +'/5')
    print('p2-' + str(s2) +'/5')

def start():
    """Choosing 1 or 2 player, making sure the correct input."""
    global multi
    multi = input('1 or 2 Players? ')
    print('\n')
    if multi.strip() == '1':
        game1()
    if multi == '2':
        game2()
    if multi.strip() in quit:
        print('Goodbye!')
        exit()
    if multi.strip() != '1' or multi != '2':
        print('Invalid response!')
        print('\n')
        start()

def single():
    """Single player against the ai"""
    global p1
    p2 = rps[(random.randint(0,2))]
    p1 = str(input('Rock, Paper, Scissors? '))
    if p1 in quit:
        quit_game()
    p1 = choice(p1)
    print('AI Chose-' + p2)
    compare(p1,p2)
    print('\n')

def game1():
    """Loop to keep single player going."""
    while True:
        single()

def game2():
    """Loop to keep two player going."""
    while True:
        dual()

def dual():
    """Two player"""
    global p1,p2
    p1 = str(input('Rock, Paper, Scissors? '))
    if p1 in quit:
        quit_game()
    p1 = choice(p1)
    p2 = str(input('Rock, Paper, Scissors? '))
    if p2 in quit:
        quit_game()
    p2 = choice(p2)
    compare(p1,p2)
    print('\n')

def choice(p):
    """can take multiple inputs to equal same value. also
    making sure valid input"""
    if p.strip() in rock:
        return 'Rock'
    if p.strip() in paper:
        return 'Paper'
    if p.strip() in scissors:
        return 'Scissors'
    else:
        print('Invalid response!')
        print('\n')
        if multi == '1':
            game1()
        if multi == '2':
            game2()

def compare(p1,p2):
    """Compares the two players."""
    global multi
    if p1 == p2:
        print("It's a Tie!")
        print('\n')
        if multi == '1':
            game1()
        if multi == '2':
            game2()
    if p1 == 'Rock' and p2 == 'Scissors' or p1 == 'Paper' and p2 == 'Rock' or p1 == 'Scissors' and p2 == 'Paper':
        scoreboard(p1=1,p2=0)
    else:
        scoreboard(p1=0,p2=1)

def scoreboard(p1,p2):
    """Adds a point appropriately."""
    global s1,s2
    if p1 == 1:
        s1 += 1
        print('Player 1 Wins!')
        win()
    if p2 == 1:
        s2 += 1
        print('AI Wins!')
        win()
    text()

def win():
    """Checks to see if either scores have reached 5."""
    global s1,s2
    if s1 == 5 or s2 == 5:
        winner()

def winner():
    """Says who won and asks for a rematch."""
    if s1 > s2:
        print('Player 1 Wins the tournament!')
        text()
        rematch()
    if s1 < s2:
        print('Player 2 Wins the tournament!')
        text()
        rematch()
    if s1 == s2:
        print("It's a Tie!")
        text()
        rematch()

def quit_game():
    """Says who won when you quit during game. Without asking for rematch."""
    global p1,p2
    if p1 in quit or p2 in quit:
        if s1 > s2:
            print('Player 1 Wins the tournament!')
            text()
            exit()
        if s1 < s2:
            print('Player 2 Wins the tournament!')
            text()
            exit()
        if s1 == s2:
            print("It's a Tie!")
            text()
            exit()

def rematch():
    """Asks for rematch and sets score to 0."""
    print('\n')
    re = input('Would you like a rematch? Yes/No ')
    if re in restart:
        print('\n')
        global s1,s2
        s1 = 0
        s2 = 0
        start()
    else:
        print('Goodbye!')
        exit()

start()

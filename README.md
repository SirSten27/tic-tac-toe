import turtle as t
from time import sleep as w

#setup
t.setup(600, 600)
t.pensize(5)
t.speed(6)

#board setup vertical
t.penup()
t.goto(-100, 300)
t.pendown()
t.goto(-100, -300)
t.penup()
t.goto(100, 300)
t.pendown()
t.goto(100, -300)
#board setup horisontal
t.penup()
t.goto(-300, 100)
t.pendown()
t.goto(300, 100)
t.penup()
t.goto(-300, -100)
t.pendown()
t.goto(300, -100)

global squareX
squareX = -200
global squareY
squareY = 200

#pieces
def cross():
	global squareX
	global squareY
	t.penup()
	t.goto(squareX + 90, squareY + 90)
	t.pendown()
	t.goto(squareX - 90, squareY - 90)
	t.penup()
	t.goto(squareX - 90, squareY + 90)
	t.pendown()
	t.goto(squareX + 90, squareY -90)

def circle():
	global squareX
	global squareY
	t.penup()
	t.goto(squareX, squareY - 90)
	t.pendown()
	t.circle(90)

global i
i = 0	
#piece order
def placepiece():
	pieceorder = ['X', 'O', 'X', 'O', 'X', 'O', 'X', 'O', 'X']
	global i
	global turn
	turn = pieceorder[i]
	if turn == 'X':
		cross()
		i = i + 1		
	elif turn =='O':
		circle()
		i = i + 1
		

field = {
'field1':0,
'field2':0,
'field3':0,
'field4':0,
'field5':0,
'field6':0,
'field7':0,
'field8':0,
'field9':0}

#detect square clicked
def squareclick(x, y):
	if x > -300 and x <  -100 and y < 300 and y > 100:
		global turn
		global squareX
		global squareY
		squareX = -200
		squareY = 200
		placepiece()
		if turn == 'X':
			field['field1'] = 1
		elif turn == 'O':
			field['field1'] = 2
		
	elif x > -100 and x < 100 and y < 300 and y > 100:
		squareX = 0
		squareY = 200
		placepiece()
		if turn == 'X':
			field['field2'] = 1
		elif turn == 'O':
			field['field2'] = 2
	elif x > 100 and x < 300 and y < 300 and y > 100:
		squareX = 200
		squareY = 200
		placepiece()
		if turn == 'X':
			field['field3'] = 1
		elif turn == 'O':
			field['field3'] = 2
	elif x > -300 and x < -100 and y < 100 and y > -100:
		squareX = -200
		squareY = 0
		placepiece()
		if turn == 'X':
			field['field4'] = 1
		elif turn == 'O':
			field['field4'] = 2
	elif x > -100 and x < 100 and y < 100 and y > -100:
		squareX = 0
		squareY = 0
		placepiece()
		if turn == 'X':
			field['field5'] = 1
		elif turn == 'O':
			field['field5'] = 2
	elif x > 100 and x < 300 and y < 100 and y > -100:
		squareX = 200
		squareY = 0
		placepiece()
		if turn == 'X':
			field['field6'] = 1
		elif turn == 'O':
			field['field6'] = 2
	elif x > -300 and x < -100 and y < -100 and y > -300:
		squareX = -200
		squareY = -200
		placepiece()
		if turn == 'X':
			field['field7'] = 1
		elif turn == 'O':
			field['field7'] = 2
	elif x < 100 and x > -100 and y < -100 and y > -300:
		squareX = 0
		squareY = -200
		placepiece()
		if turn == 'X':
			field['field8'] = 1
		elif turn == 'O':
			field['field8'] = 2
	elif x < 300 and x > 100 and y < -100 and y > -300:
		squareX = 200
		squareY = -200
		placepiece()
		if turn == 'X':
			field['field9'] = 1
		elif turn == 'O':
			field['field9'] = 2	

#win conditions
def wincondition():
#vertical
	try:
		if field['field1'] == field['field4'] == 			field['field7'] != 0:
			return 1
	
		if field['field2'] == field['field5'] == field['field7'] != 0:
			return 2
		
		if field['field3'] == field['field6'] ==  field['field9'] != 0:
			return 3

#horisontal	
		if field['field1'] == field['field2'] == field['field3'] != 0:
			return 4
	
	
#winner
		winner = wincondition()
		if winner == 11:
			t.penup()
			t.goto(-200, 200)
			t.pendown()
			t.goto(-200, -200)

		t.onscreenclick(squareclick)
		t.listen()
		t.exitonclick()	

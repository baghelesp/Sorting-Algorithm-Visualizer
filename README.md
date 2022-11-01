# Sorting-Algorithm-Visualizer
This is a small python project to visualize the flow of different sorting algorithms and  traces the changes occurring in the position of elements of the array.
## PROBLEM STATEMENT
Visualization of major sorting algorithms using Python Library ‘Tkinter’.
## EXPLANATION OF ASSIGNMENT
Various sorting algorithms are present and many of which are taught in colleges, but
even if the teacher tries their best to make the students explain, it always lacks a vital
element i.e visualization. So here we present our group project SORTING
ALGORITHMS TRACER.
### PROGRAMMING LANGUAGE AND TOOLS USED
This project uses a python standard GUI library 'Tkinter'. The Tkinter module helps in
creating GUI applications in a fast and easy way.
Some common ones are Buttons, Labels, Frames, Menus. The message, Radio button,
Text, Scrollbar, and so on.
Some of the advantages of using Tkinter include -
Tkinter provides three geometry managers: place, pack, and grid. That is much
more powerful and easy to use.
Tkinter is more flexible and stable.
It has standard attributed dimensions, fonts, colours, cursors, anchors, and bitmaps
for a better GUI.
## PROGRAM CODE
### main.py
```python
from cProfile import label
# from signal import pause
from tkinter import *
from tkinter import ttk
import random
from time import time,sleep
from Helper.color import *
# import itertools
# import operator
from Algorithms.Bubble_Sort import bubble_sort
from Algorithms.Selection_Sort import selection_sort
window = Tk()
window.title("Sorting Algorithms Visualization")
window.maxsize(1000, 700)
window.config(bg = LIGHT_GRAY)
algorithm_name = StringVar()
algo_list = ['Bubble Sort','Selection Sort']
speed_name = StringVar()
speed_list = ['Fast', 'Medium', 'Slow']
data = []
# toggle_pause_unpause = itertools.cycle(["pause","unpause"])
# def on_pause_unpause_button_clicked(self):
# action = next(self.toggle_pause_unpause)
# if action == 'pause' :
# self.player.pause()

# elif action == 'unpause':
# self.player.unpause()
def drawData(data, colorArray):
canvas.delete("all")
canvas_width = 800
canvas_height = 400
x_width = canvas_width / (len(data) + 1)
offset = 10
spacing = 5
normalizedData = [i / max(data) for i in data]
for i, height in enumerate(normalizedData):
x0 = i * x_width + offset + spacing
y0 = canvas_height - height * 390
x1 = (i + 1) * x_width + offset
y1 = canvas_height
canvas.create_rectangle(x0, y0, x1, y1, fill = colorArray[i])
canvas.create_text((x0+x1)/2, (y0+y1)/2,text=int(height*max(data)),fill="white",fo
nt=('Helvetica 15 bold'))
window.update_idletasks()
# randome values generate
def generate():
global data
data = []
for i in range(0, 10):
random_value = random.randint(1, 150)
data.append(random_value)
drawData(data, [BLUE for x in range(len(data))])
def set_speed():
if speed_menu.get() == 'Slow':
return 0.999
elif speed_menu.get() == 'Medium':
return 0.6
else:
return 0.003
def get_input():
global data
global inputtxt
data = []
l4 = Label(UI_frame, text = "", bg = LIGHT_GRAY, fg = RED)
l4.grid(row = 5, column = 0, padx = 10, pady = 5, sticky = W)
data = [int(x) for x in inputtxt.get().split()]
drawData(data, [BLUE for x in range(len(data))])

# algo sleect karna and speed initialise
def sort():
global data
timeTick = set_speed()
if algo_menu.get() == 'Bubble Sort':
bubble_sort(data, drawData, timeTick)
elif algo_menu.get() == 'Selection Sort':
selection_sort(data, drawData, timeTick)
UI_frame = Frame(window, width = 10, height = 300, bg = YELLOW)
UI_frame.grid(row = 0, column = 0, padx = 100, pady = 50)
# dropdown to select sorting algorithm
l1 = Label(UI_frame, text = "Algorithm: ", bg = LIGHT_GRAY, fg = RED, font=("Helvetica bol
d", 12))
l1.grid(row = 0, column = 0, padx = 10, pady = 5, sticky = W)
algo_menu = ttk.Combobox(UI_frame, textvariable = algorithm_name, values = algo_list)
algo_menu.grid(row = 0, column = 1, padx = 5, pady = 5)
algo_menu.current(0)
l2 = Label(UI_frame, text = "Sorting Speed: ", bg = LIGHT_GRAY, fg = BLUE, font=("Helvetic
a bold", 12))
l2.grid(row = 1, column = 0, padx = 10, pady = 5, sticky = W)
speed_menu = ttk.Combobox(UI_frame, textvariable = speed_name, values = speed_list)
speed_menu.grid(row = 1, column = 1, padx = 5, pady = 5)
speed_menu.current(0)
# t inputt
l3 = Label(UI_frame, text = "Enter your Nums: ", bg = LIGHT_GRAY, fg = PURPLE, font=("Helv
etica bold", 12))
l3.grid(row = 2, column = 0, padx = 10, pady = 5, sticky = W)
inputtxt = Entry(UI_frame, width = 30)
inputtxt.grid(row = 2, column = 1, padx = 5, pady = 5)
b2 = Button(UI_frame, text = "Generate Nums", command = generate, bg = YELLOW, fg = LIGHT_
GRAY, font=("Helvetica bold", 11))
b2.grid(row = 4, column = 0, padx = 5, pady = 5)
b1 = Button(UI_frame, text = "Sort", command = sort, bg = YELLOW, fg = LIGHT_GRAY, font=
("Helvetica bold", 11))
b1.grid(row = 4, column = 1, padx = 5, pady = 5)
b3 = Button(UI_frame, text = "Use your Nums", command = get_input, bg = YELLOW, fg = LIGHT
_GRAY, font=("Helvetica bold", 11))
b3.grid(row = 4, column = 2, padx = 5, pady = 5)

# b4=Button(UI_frame,text="Pause/Resume",command=on_pause_unpause_button_clicked('unpaus
e'),bg=RED,fg=WHITE,font=("Helvetica bold", 11))
# b4.grid(row=4,column=3,padx=5,pady=5)
# b4=Button(UI_frame,text="Pause/Resume",command=start_stop,bg=RED,fg=WHITE,font=("Helveti
ca bold", 11))
# b4.grid(row=4,column=3,padx=5,pady=5)
# making canvas
canvas = Canvas(window, width = 800, height = 400, bg = LIGHT_GRAY)
canvas.grid(row = 1, column = 0, padx = 10, pady = 5)
window.mainloop()
bubble_sort.py
# We need the time module to create some time difference between each comparison
import time
# Importing colors from colors.py
from Helper.color import *
def bubble_sort(data, drawData, timeTick):
size = len(data)
for i in range(size - 1):
for j in range(size - i - 1):
if data[j] > data[j +1]:
data[j], data[j + 1] = data[j + 1], data[j]
drawData(data, [YELLOW if x == j or x == j+1 else BLUE for x in range(len
(data))] )
time.sleep(timeTick)
drawData(data, [BLUE for x in range(len(data))])
selection_sort.py

# We need the time module to create some time difference between each comparison
import time
# Importing colors from colors.py
from Helper.color import *
def selection_sort(data, drawData, timeTick):
for i in range(len(data) - 1):
Min_Idx = i
for k in range(i + 1, len(data)):
if data[k] < data[Min_Idx]:
Min_Idx = k
data[Min_Idx], data[i] = data[i], data[Min_Idx]
drawData(data, [YELLOW if x == Min_Idx or x == i else BLUE for x in range(len(dat
a))])
time.sleep(timeTick)
drawData(data, [BLUE for x in range(len(data))])
```
### color.py
```python
DARK_GRAY = '#16252C'
LIGHT_GRAY = '#1A1919'
BLUE = '#0CA8F6'
DARK_BLUE = '#0439CC'
WHITE = '#FFFFFF'
BLACK = '#000000'
RED = '#F22810'
YELLOW = '#BDB328'
PINK = '#F50BED'
LIGHT_GREEN = '#05F50E'
PURPLE = '#BF01FB'
DARK_GREEN = '#19631B'
```
## OUTPUT (Bubble Sort)
Initial screen (input array to sort) →

The output window while performing sorting (in this case Bubble
Sort with SLOW as speed parameter) →

Final Output (displays sorted array) →

## PROJECT OUTCOME
Through this assignment, we were able to successfully create a project using Tkinter in
Python.
By using Tkinter Library of python we learnt the use of Tkinter to display graphical
figures of data sets like charts and other figures and manipulation of these figures.
This project also cleared the concepts of sorting and we also understood the flow of
different sorting algorithms through visualization of these sorting algorithms.
Also while working on this project we learnt and developed various qualities like working
in a team, Time Management, etc. leading to the successful and timely completion of
the assignment.

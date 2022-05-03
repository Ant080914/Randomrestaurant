from lib2to3.pgen2 import driver
from tkinter import *
import random
from turtle import bgcolor
from unittest import result
import winreg
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.common.by import By
from time import sleep
import geocoder

# Add radiobuttons to ask if you want use all the restrauants in the area or your list
win = Tk()
win.title(' Random Resaurant')
win.geometry('1500x400')
win.config(background='darkgray')

Greeting = Label(win, text="Random Resaurant", font="Times" "24" "Bold", bg='darkgray')
Greeting.place(relx=0.5, rely=0.0, anchor='n')

intro = Label(win, text="List the desired resaurants and we will pick one randomly for you and provide you with dirctions and contact infromation.", font="Times" "15", bg='darkgray')
intro.place(relx = 0.18, rely = 0.1, anchor=W)

name = Label(win, text='Resaurant name: ', font='Times' '10', bg = 'darkgray')
name.place(relx = 0.0, rely = 0.5, anchor = W )

e1 = Entry(win, width=50, fg = 'black', font= "Times" '10')
e1.place(relx=0.1, rely = 0.5, anchor=W)

def btn():
  resaurant.append(e1.get())
  e1.delete(0, END)
  
resaurant=[]

btn1 = Button(win, text="Add", bg="darkgray", font='Times', width=7, height=1, command=btn)
btn1.place(relx=0.50, rely=0.5, anchor=CENTER)  

def resize(event):
  print("New size is: {}x{}".format(event.width, event.height))

def run():
 win.destroy()
 
 win2=Tk()
 win2.geometry('800x800')
 win2.title("Results")
 win2.config(bg='darkgray')
 
 go = random.choice(resaurant)
 
 results=Label(win2,text='Your randomly selected restaurant is: ' + go, font='Times' '16', bg='darkgray')
 results.place(relx=0.5, rely=0.0, anchor=N)

 City = Label(win2, text='City: ', bg='darkgray', font= 'Times' '16')
 City.place(relx=0.1, rely=0.1, anchor=W)

 e2 = Entry(win2, width=50, fg='black', font='Times' '16')
 e2.place(relx=0.2,rely=0.1, anchor=W)

 State = Label(win2, text='State: ', bg='darkgray', font= 'Times' '16')
 State.place(relx=0.1, rely=0.2, anchor=W)

 e3 = Entry(win2, width=50, fg='black', font='Times' '16')
 e3.place(relx=0.2,rely=0.2, anchor=W)
 
 def search():
   city = e2.get()
   state = e3.get()
   win2.destroy()
   
   g = geocoder.ip('me')
   location = (str(g.latlng))
   driver=webdriver.Chrome('C:/Users/alexn/OneDrive/Documents/Chrome/Chromedriver')
   driver.maximize_window()
   driver.get('https://www.google.com/maps/@39.6329326,-100.596812,5z')
   sleep(2)
   
   Place=driver.find_element(By.XPATH, ' //*[@id="searchboxinput"]').send_keys( go + " " + " " + city + " " + state)
   Ran = driver.find_element(By.XPATH,' //*[@id="searchbox"]/div[1]').click()
  
   
   sleep(60)
   
 btn3 = Button(win2, text='Submit', font='Times' '16', bg='darkgray',command=search)
 btn3.place(relx=0.52, rely=0.3, anchor=CENTER)
 
 win2.mainloop()
 

btn2 = Button(win, text="Run", bg="darkgray", font='Times', width=7, height=1, command=run)
btn2.place(relx=0.56, rely= 0.5, anchor=CENTER)

win.mainloop()

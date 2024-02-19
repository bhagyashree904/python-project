# python-project
from tkinter import *
from tkinter import ttk
class todo:
    def __init__(self,root):
        self.root= root
        self.root.title("TO-DO-LIST")
        self.root.maxsize(width=1300,height=700)
        self.root.minsize(width=1100,height=700)
        #self.root.geometry("410x650+300+150")
        self.root["bg"] = "grey"

        Image_icon = PhotoImage(file="C:/Users/bhagy/Pictures/download.png")
        root.iconphoto(False, Image_icon)

        self.label = Label(self.root,text="    TO-DO-LIST-APP ",font="ariel  25 bold ",width=20,bd=20,bg='orange',fg='black')
        self.label.pack(side='top',fill=BOTH)

        self.label1 = Label(self.root, text=" Enter the Task :", font="ariel  18 bold ", width=13, bd=5, bg='orange',
                           fg='black')
        self.label1.place(x=70,y=100)

        self.label4 = Label(self.root, text=" Tasks ", font="ariel  18 bold ", width=10, bd=5, bg='orange',
                            fg='black')
        self.label4.place(x=470, y=100)

        self.main_text = Listbox(self.root, font="ariel  18 italic bold ", width=55, bd=15, height=9)
        self.main_text.place(x=300, y=150)

        self.text = Text(self.root, font="ariel  18 italic bold ", width=15, bd=5, height=2)
        self.text.place(x=70, y=150)

        def add():
            content = self.text.get(1.0,END)
            self.main_text.insert(END,content)
            with open('data.txt', 'a') as file:
                file.write(content)
                file.seek(0)
                file.close()
        self.text.delete(1.0,END)

        def delete():
            delete_ = self.main_text.curselection()
            look =self.main_text.get(delete_)
            with open('data.txt', 'r+') as f:
                new_f = f.readlines()
                f.seek(0)
                for line in new_f:
                    item=str(look)
                    if item not in line:
                        f.write(line)
                f.truncate()
            self.main_text.delete(delete_)


        self.button=Button(self.root,text='ADD',font='sarif 20 bold italic',width=10,bd=5,bg='orange',fg='black',command=add)
        self.button.place(x=70,y=250)
        self.button2 = Button(self.root, text='DELETE', font='sarif 20 bold italic', width=10, bd=5, bg='orange',
                             fg='black', command=delete)
        self.button2.place(x=70,y=350)

def main():
    root=Tk()
    ui=todo(root)
    root.mainloop()

if __name__ =="__main__":
    main()

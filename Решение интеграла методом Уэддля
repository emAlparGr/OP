import numpy as np
import matplotlib.pyplot as plt
from tkinter import *
import time
from tkinter import messagebox
from matplotlib.backends._backend_tk import NavigationToolbar2Tk
from matplotlib.backends.backend_tkagg import FigureCanvasTkAgg
from matplotlib.figure import Figure

def f(x, ans):
    if ans == 1:
        return 1-x**3
    elif ans == 2:
        return 2-5*x**2
    elif ans == 3:
        return 3-8*x**6+5


def prin(a, b, e, ans):

    try:
        a=float(a)
        b=float(b)
        e=float(e)
    except ValueError:
        messagebox.showinfo('Ошибка', f'Параметры введены неверно')
        return 0

    if e < 0:
        messagebox.showinfo('Ошибка', f'Точно не может быть меньше 0.')
        return 0
    elif a > b:
        messagebox.showinfo('Ошибка', f'Начало отрезка не может быть больше его конца')
        return 0

    fig.clf()
    res, n = runge(e, a, b, 6, ans)
    N.config(text=f"Количество разбиений: {n}")
    label_result.config(text="Ответ = %.4f" % res)
    plot1 = fig.add_subplot(1, 1, 1)
    i = a
    x = np.linspace(a, b, 200)
    h = (b - a) / n
    plot1.grid(axis='both')
    plt.clf()
    ym=f(b,ans)

    plt.ion()
    plot1.axvline(x=0, c='black',markersize=5)
    plot1.axhline(y=0, c='black',markersize=5)
    plot1.plot(x, f(x, ans), linewidth=2,color='blue')
    while i < b:
        canvas.draw()
        plot1.vlines(x=i, ymin=ym,ymax=f(i,ans), colors='green')
        i += h
        time.sleep(0.2)
        canvas.flush_events()
    canvas.draw()
    plt.ioff()


def weddle1(a, b, n, ans):
    h = (b - a) / n
    summa = 0
    for __ in range(n // 6):
        summa += f(a, ans) + 5 * f(a + h, ans) + f(a + 2 * h, ans) + 6 * f(a + 3 * h, ans) + f(a + 4 * h, ans) + 5 * f(
            a + 5 * h, ans) + f(a + 6 * h, ans)
        a += 6 * h
    return summa * (3 * h / 10)


def runge(eps, a, b, n, ans):

    ex = 0
    W2 = weddle1(a, b, n, ans)
    while ex == 0:
        W1 = W2
        n = n * 2
        W2 = weddle1(a, b, n, ans)
        E = abs(W1 - W2) / 63
        if (E < eps):
            return (weddle1(a, b, n, ans)), n
            ex = 1

def main():
    global canvas, fig, label_result, N
    window = Tk()
    window.title("Решение интеграла методом Уэддля")
    window.geometry('900x500')

    fig = Figure(figsize=(4, 4), dpi=100)
    canvas = FigureCanvasTkAgg(fig, master=window)
    canvas.get_tk_widget().place(x=435, y=20)
    toolbar = NavigationToolbar2Tk(canvas, window)
    toolbar.update()
    toolbar.place(x=400, y=400)
    Label(window, text="Выберите функцию:", font=("Arial Bold", 15)).place(x=10, y=50)

    r_var = IntVar()
    r_var.set(1)
    Radiobutton(window, text='1-х^3', variable=r_var, value=1, font=("Arial Bold", 12)).place(x=250, y=50)
    Radiobutton(window, text='2-5*x^2', variable=r_var, value=2, font=("Arial Bold", 12)).place(x=250, y=20)
    Radiobutton(window, text='3-8*x^6+5', variable=r_var, value=3, font=("Arial Bold", 12)).place(x=250, y=80)

    label_result = Label(window, font=("Arial Bold", 15))
    label_result.place(x=10, y=210)

    N = Label(window, font=("Arial Bold", 15))
    N.place(x=10, y=240)

    Label(window, text="Введите начало отрезка:", font=("Arial Bold", 15)).place(x=10, y=150)
    a = Entry(window, width=15)
    a.insert(0, "0")
    Label(window, text="Введите конец отрезка:", font=("Arial Bold", 15)).place(x=10, y=180)
    b = Entry(window, width=15)
    b.insert(0, "5")
    Label(window, text="Введите точность:", font=("Arial Bold", 15)).place(x=10, y=120)
    e = Entry(window, width=15)
    e.insert(0, "0.01")
    a.place(x=250, y=156)
    b.place(x=250, y=186)
    e.place(x=250, y=128)
    button_on = Button(text="Решить", font=("Arial Bold", 15),command=lambda: prin(a.get(), b.get(), e.get(), r_var.get()))
    button_on.pack(side=BOTTOM)


    window.mainloop()


if __name__ == '__main__':
    main()

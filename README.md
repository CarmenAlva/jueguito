# jueguito
from random import randrange
from Tkinter import *
import sys

def dibujar_muneco(opcion):
if opcion == 1:
# CREAR EL YUGO
C.create_line(580, 150, 580, 320, width=4, fill="blue")
# CREAR LA CABEZA
C.create_oval(510, 150, 560, 200, width=2, fill='PeachPuff')

if opcion == 2:
    # CREAR EL TRONCO
    C.create_line(535, 200, 535, 290, width=2)

if opcion == 3:
    # CREAR LA PIERNA IZQUIERDA
    C.create_line(535, 290, 510, 320, 500, 320, width=2)

if opcion == 4:
    # CREAR LA PIERNA DERECHA
    C.create_line(535, 290, 560, 320, 550, 320, width=2)

if opcion == 5:
    # CREAR LA MANO IZQUIERDA
    C.create_line(535, 230, 510, 250, 500, 250, width=2)

if opcion == 6:
    # CREAR LA MANO DERECHA
    C.create_line(535, 230, 560, 250, 550, 270, width=2)

if opcion == 7:
    # CREAR LA SOGA
    C.create_line(510, 210, 580, 210,width=4, fill="blue")
def obtener_palabra():
global adivinar, oportunidades, fin_juego, numerradas, palabra, digitadas

# APERTURA DEL ARCHIVO DE PALABRAS (117 PA�SES)
# SOLO LECTURA
try:
fp = open ("C:\Mis documentos\LabLeng II\Pa�ses.txt","r")
except IOError:
print "NO SE PUDO ABRIR EL ARCHIVO. VERIFIQUE EL PATH O SI EL ARCHIVO EXISTE"
sys.exit()

# OBTENCI�N DE UN N�MERO ALEATORIO.
num = randrange(1,118,1)

# ADIVINAR ES LA PALABRA QUE SE VA A TOMAR DEL ARCHIVO DE PALABRAS Y QUE
# EL USUARIO DEBE ADIVINAR.
for i in range (1,118,1):
    if i == num:
        adivinar = (fp.readline()).split(" ")
    else:
        fp.readline()
fp.close()

# LISTA MOSTRADA EN PANTALLA PARA LA PALABRA A ENCONTRAR
palabra = [" ", " ", " ", " ", " ", " ", " ", " ", " ", " ", " ", " ", " "]

# LISTA CON LAS LETRAS ERRADAS DIGITADAS POR EL USUARIO
digitadas = [" ", " ", " ", " ", " ", " ", " "]

#VARIABLES DEL JUEGO
oportunidades = 7
fin_juego = 0
# N�MERO DE LETRAS ERRADAS DIGITADAS
numerradas = 0

i = 0
while i<len(adivinar) - 1:
palabra[i] = '_'
i = i + 1

# J: PARA COLOCAR LA LETRA J PIXELES A LA DERECHA.
i = 0
j = 0 
while i<len(adivinar) - 1:
    C.create_text(50 + j, 200, text = palabra[i], font='Times', fill='blue')
    j = j + 20
    i = i + 1
def ahorcado():
global letra, oportunidades, adivinar, fin_juego, numerradas, palabra, digitadas

i = 0
contar_letras = 0
while i<len(adivinar) - 1:
if adivinar[i] == letra.get():
    palabra[i] = letra.get()
    contar_letras = 1
i = i + 1

if contar_letras == 0:
oportunidades = oportunidades - 1
digitadas[numerradas] = letra.get()
numerradas = numerradas + 1
    
i = 0
j = 0 
while i<len(palabra) - 1:
C.create_text(50 + j, 200, text = palabra[i], font='Times', fill='blue')
j = j + 20
i = i + 1

i = 0
j = 0 
while i<len(digitadas) - 1:
C.create_text(50 + j, 320, text=digitadas[i], font='Times', fill='blue')
j = j + 20
i = i + 1

if numerradas == 1:
    dibujar_muneco(1)
if numerradas == 2:
    dibujar_muneco(2)
if numerradas == 3:
    dibujar_muneco(3)
if numerradas == 4:
    dibujar_muneco(4)
if numerradas == 5:
    dibujar_muneco(5)
if numerradas == 6:
    dibujar_muneco(6)
if numerradas == 7:
    dibujar_muneco(7)
    
# VERIFICAR SI PERDI�
if oportunidades == 0:
    C.create_text(75, 370, text="PERDISTE", font='Times 10 bold', fill='blue')
    C.create_text(100, 400, text="LA PALABRA ERA", font='Times 10 bold', fill='blue')
    i = 0
    j = 0 
    while i<len(adivinar) - 1:
        C.create_text(50 + j, 420, text=adivinar[i], font='Times 10 bold', fill='blue')
        j = j + 20
        i = i + 1
    boton.tkButtonLeave()

# VERIFICAR SI GAN�
i = 0
lleno = 0
while i < len(palabra) - 1:
    if palabra[i] != '_':
        lleno = lleno + 1
    i = i + 1

if lleno == len(palabra) - 1:
    C.create_text(75, 370, text="ADIVINO!!!", font='Times 10 bold', fill='blue')
    boton.tkButtonLeave()

entrada.delete(0,END)
JUEGO
root = Tk()
tex1 = 'JUEGO DEL AHORCADO\nPAISES DEL MUNDO\nREALIZADO POR\nJHON ALEXANDER CAMACHO'
tex2 = '\n\nA B C D E F G H I J K L M N O P Q R S T U V W X Y Z'
C = Canvas(root, width=600, height=450, background='LightYellow')
C.create_text(300, 70, justify='center', text=tex1+tex2, font='Times 10 bold', fill='blue')

ELEMENTOS A COLOCAR EN EL CANVAS
letra = StringVar()
solicitud = Label(root, text="DIGITE UNA LETRA: ")
entrada = Entry(root, textvariable = letra)
boton = Button(root, text = " J U G A R ", command = ahorcado, width=20)
botonsalida = Button(root, text = "S A L I R", command=C.quit, width=20)
C.grid(row=1, column=1, columnspan=4)
solicitud.grid(row=2, column=1)
entrada.grid(row=2, column=2)
boton.grid(row=2, column=3)
botonsalida.grid(row=2, column=4)

SE OBTIENE LA PALABRA A ADIVINAR
obtener_palabra()

root.mainloop()

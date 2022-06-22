import random
import time

print("-"*80)
print("                                 HANGMAN GAME")
print("-"*80)
print( )
print("Bienvenidos al juego 'Hangman game'")
print( )
time.sleep(2)
print("-----------------------------------------------\n             Instrucciones de como jugar\n-----------------------------------------------\n")
print("1. Al iniciar el juego se te asigna una palabra aleatoria, debes intentar adivinarla letra por letra hasta completarla\n")
print("2. Tendras 7 vidas, las cuales se pierden si ingresas una letra incorrecta ")
print('='*100)

# Lectura de archivo que contiene las palabras
def archivo(): 
    palabras=[]
    with open("random.txt","r") as archivo:
        for linea in archivo:
            palabras.append(linea.rstrip())
        return random.choice(palabras)
        
palabra= archivo()
print('_ ' * len(palabra.lower())) # Muestra los espacios/cantidad de letras que posee la palabra
print( )

intentos= 7 # Cantidad de intentos que tendra el usuario
letras=[]   

while True:
    # Letras adivinadas
    letra_adv = input("Adivina una letra: ")       # Solo se puede ingresar letras 
    if len(letra_adv)!=1 and letra_adv.isalnum() : # si el jugador ingresa un caracter distintos a una letra 
        print("Por favor solo ingrese una letra")  # se le mostrara el mensaje
    elif letra_adv.isdigit():
        print("Lo ingresado no es una letra, por favor intentelo denuevo")
    else:
        if letra_adv.lower() in letras:
            print("Esta letra ya fue ingresada, intenta con otra por favor")
        else:
            letras.append(letra_adv.lower())
 
        if letra_adv.lower() in palabra:
            print( )
            print("¡¡Felicidades!! Adivinaste una letra\n*Aún tienes ", str(intentos),"intentos")
            print( )
            break
        else:
            intentos = intentos-1
            print( )
            print("Ups! Esta letra es incorrecta. Haz perdido un intento")
            print("*Te quedan " + str(intentos) + " intentos")
            print( )
            break

    # Si al jugador no le quedan intentos entonces pierde el juego 
    if intentos==0:
        print("-"*80)
        print("                                   GAME OVER")
        print('-'*80)
        print("\nHaz perdido todos tus intentos\n \nLa palabra secreta era: ", palabra)
        print( )
        print('-'*75)
        break
 
 
    condicion = "" # Estado/actualizacion de la palabra 
 
    letra_fal = 0 # Letras faltantes
    for letra in palabra:
 
        if letra in letras:
            condicion = condicion + letra
    
        else:
            condicion = condicion + "_"
            letra_fal = letra_fal + 1
 
    # Imprimir palabra con las letras adivinadas
    print(condicion)
 
    if letra_fal == 0: # Si no faltan letras por adivinar el jugador Gana 
        print( )
        print("-"*60)
        print( )
        print("Felicidades!!! Haz adivinado la palabra \nLa palabra secreta es: ", palabra)
        break

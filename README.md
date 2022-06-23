import random
import time

#Entradas: random.txt, palabra= archivo(), input letra_adv, letra
#Salidas: return random.choice(palabras), letra_fal, print('_ ' * len(palabra.lower())), print(mensaje)

#Lista de palabras para adivinar
lista= open("random.txt", "r")

#Bienvenida, intrucciones y reglas del juego
print('='*100)
print("                                 HANGMAN GAME")
print('='*100)
print("\n                      ¡BIENVENID@S A 'HANGMAN GAME'!\n" )
print('='*100)
print()
time.sleep(2)

#=====================================================================#
#                             Intrucciones                            #
#=====================================================================#

print("-----------------------------------------------\n             Instrucciones de como jugar\n-----------------------------------------------\n")
print("1. Al iniciar el juego se te asigna una palabra aleatoria, debes intentar adivinarla letra por letra hasta completarla\n")
print("2. Tendras 7 intentos los cuales se pierden si ingresas una letra incorrecta\n")
print('='*100)


#Cantidad de intentos que tendra el usuario
intentos= 7

#Letras adivinadas
letras=[]

#Palabra secreta
def archivo():
    palabras=[]
    with open("random.txt","r") as archivo:
        for linea in archivo:
            palabras.append(linea.rstrip())
        return random.choice(palabras)


palabras=archivo()
print('_ ' * len(palabras.lower())) #Muestra los espacios/cantidad de letras que posee la palabra
print( )

#Bucle principal
while True:
    while True:
        
        adivina_letra = input("Adivina una letra: ")
        if len(adivina_letra)!=1 and adivina_letra.isalnum() :
            print("Por favor solo ingrese una letra")
        elif adivina_letra.isdigit():
            print("Lo ingresado no es una letra, por favor intentelo denuevo")
        else:
            if adivina_letra.lower() in letras:
                print("Esta letra ya fue ingresada, intenta con otra por favor")
            else:
                letras.append(adivina_letra.lower())
 
                if adivina_letra.lower() in palabras:
                    print( )
                    print("¡¡Felicidades!! Adivinaste una letra\n*Aún tienes " + str(intentos) + " intentos")
                    print( )
                    break
                else:
                    intentos = intentos-1
                    print( )
                    print("Ups! Esta letra es incorrecta. Haz perdido un intento")
                    print("*Te quedan " + str(intentos) + " intentos")
                    print( )
                    break

    if intentos==0:
        print("-"*80)
        print("                                   GAME OVER")
        print('-'*80)
        print("\nHaz perdido todos tus intentos\n \nLa palabra secreta era: ", palabras)
        print( )
        print("----------------------")
        print(":                    :")
        print(":                    0")
        print(":                  \ | /")
        print(":                    |")
        print(":                   / \ ")
        print(":")
        print(":")
        print("-----------------------")
        print('-'*75)
        break
 
 
    condicion = ""
 
    letras_fallidas = 0
    for letra in palabras:
 
 
        if letra in letras:
            condicion = condicion + letra
 
        else:
            condicion = condicion + "_"
            letras_fallidas = letras_fallidas + 1
 
    ## Imprimir palabra con las letras adivinadas
    print(condicion)
 
 
    if letras_fallidas == 0:
        print( )
        print("-"*60)
        print( )
        print("Felicidades!!! Haz adivinado la palabra \nLa palabra secreta es: ", palabras)
        break

